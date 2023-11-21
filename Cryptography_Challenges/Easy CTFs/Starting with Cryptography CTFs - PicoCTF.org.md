
Taken from: https://picoctf.org

-----------------------------------------------------------------------------------

## Challenge Mod 26

Description:
```
Cryptography can be easy, do you know what ROT13 is? 
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_nSkgmDJE}
```

We can try to use the ROTation decoder, with -13 steps: https://www.dcode.fr/rot-cipher

And we are rewarded whit the flag:
```
picoCTF{next_time_I'll_try_2_rounds_of_rot13_aFxtzQWR}
```


-----------------------------------------------------------------------------------

## Challenge 13

Description:
```
Cryptography can be easy, do you know what ROT13 is? 
cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}
```

We can try to use the ROTation decoder, with -13 steps. This time we can code it in python:
```python
import string

ALPHABET = list(string.printable)
LEN = len(ALPHABET)

cipher = '''cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}'''
inner_cipher = '''abg_gbb_onq_bs_n_ceboyrz'''   # cause cvpbPGS == picoCTF
												# We find at Step=13 not1too1BAD1oF1A1proBLEM

def rot13_decoder(text, pos):
	rot13_decode = ''
	for c in text:
		i = ALPHABET.index(c)
		rot13_decode += ALPHABET[(i+pos)%LEN]
	return rot13_decode
	
for i in range(-30, +30):
	decoded = rot13_decoder(inner_cipher, i)
	decoded = decoded.replace('1', '_')
	print(f"Step={i}\t{decoded}")
```
We find "something" readable at pos +13, but if we submit 
`picoCTF{not1too1BAD1oF1A1proBLEM}`
They'll refuse it.

Therefore, since in the cipher text there are underscores between words, instead of 1s, we can replace them and submit the new flag:
```
decoded = decoded.replace('1', '_')
```

Finally, we have the right flag:
```
picoCTF{not_too_BAD_oF_A_proBLEM}
```


-----------------------------------------------------------------------------------

## Challenge Mind your Ps and Qs

Description
```
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? 
values= https://mercury.picoctf.net/static/12d820e355a7775a2c9129b2622a7eb6/values
```

The values that they give are:
```
Decrypt my super sick RSA:
c: 843044897663847841476319711639772861390329326681532977209935413827620909782846667
n: 1422450808944701344261903748621562998784243662042303391362692043823716783771691667
e: 65537
```

As the same for (Starting with Cryptography CTFs - CTFlearn.com/ RSA Noob - Challenge 120), we can use an online RSA decoder to decode it: https://www.dcode.fr/rsa-cipher

If we decode it, we are rewarded with the flag:
```
picoCTF{sma11_N_n0_g0od_00264570}
```

-----------------------------------------------------------------------------------

## Challenge caesar

Description:
```
Decrypt this message:
https://jupiter.challenges.picoctf.org/static/7d707a443e95054dc4cf30b1d9522ef0/ciphertext.
```

If we open the downloaded file:
```
picoCTF{gvswwmrkxlivyfmgsrhnrisegl}
```

Like the title says, we can try to use an Ceasar cracker, and brake "gvswwmrkxlivyfmgsrhnrisegl":
```python
cipher = '''gvswwmrkxlivyfmgsrhnrisegl'''

def ceasar_cracker(text, from_ = -30, to_=+30):
	for i in range(from_, to_): #possible keys [-30, 30]
		#decode
		curr_step = ''.join([chr(ord(c) + i) for c in text])
		#print
		print(f"Step={i}\t{curr_step}")

decoded = ceasar_cracker(cipher)

print(decoded)
```

If we look closely to the output, we find "something" readable at step -4: `crossingtherubicondjneoach`

If we wrap it between picoCTF{}, we'll find our flag:
```
picoCTF{crossingtherubicondjneoach}
```

-----------------------------------------------------------------------------------

## Challenge Mod 26

Description:
```
Cryptography can be easy, do you know what ROT13 is? 
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_nSkgmDJE}
```

We can try to use the ROTation decoder, with -13 steps: https://www.dcode.fr/rot-cipher

And we are rewarded whit the flag:
```
picoCTF{next_time_I'll_try_2_rounds_of_rot13_aFxtzQWR}
```


-----------------------------------------------------------------------------------
