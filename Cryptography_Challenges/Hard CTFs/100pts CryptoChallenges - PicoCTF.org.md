
## Basic-mod1

#### Description
```
We found this weird message being passed around on the servers, we think we have a working decryption scheme.
Download the message here: https://artifacts.picoctf.net/c/129/message.txt.

Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.

Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)

```

message.txt content:
```
350 63 353 198 114 369 346 184 202 322 94 235 114 110 185 188 225 212 366 374 261 213
```

```
cipher = '''350 63 353 198 114 369 346 184 202 322 94 235 114 110 185 188 225 212 366 374 261 213'''

def alphabet_decimal(number):
	if number == 36:
		return '_'
	elif number <= 25:
		return chr(number + 65) # +65 move the 0-indexed value to the first uppercase letter of the ASCII table
	elif number > 25:
		return dic[number] # +48 move the 0-indexed value to the first number of the ASCII table

  
dic = {26:0, 27:1, 28:2, 29:3, 30:4, 31:5, 32:6, 33:7, 34:8, 35:9}

listed_items = [350, 63, 353, 198, 114, 369, 346, 184, 202, 322, 94, 235, 114, 110, 185, 188, 225, 212, 366, 374, 261, 213]


# Take each number mod 37

for n in range(len(listed_items)):
	listed_items[n] = listed_items[n] % 37

#print(listed_items) #Debug print


flag = [len(listed_items)]
flag = (alphabet_decimal(listed_items[n]) for n in range(len(listed_items)))

print(list(flag))
```

If we print list(flag), we'll have this output:
```
['R', 0, 'U', 'N', 'D', '_', 'N', '_', 'R', 0, 'U', 'N', 'D', '_', 'A', 'D', 'D', 1, 7, 'E', 'C', 2]
```

If we wrap it in pioCTF{}, we'll have the flag:
```
picoCTF{R0UND_N_R0UND_ADD17EC2}
```

-----------------------------------------------------------------------------------

## Morse-code
#### Description
```
Morse code is well known. Can you decrypt this?Download the file: https://artifacts.picoctf.net/c/79/morse_chal.wav Wrap your answer with picoCTF{}, put underscores in place of pauses, and use all lowercase.
```

It can be done with Python, but I prefered to use an online decoder:
https://databorder.com/transfer/morse-sound-receiver/

If we upload the .wav file and play it, it'll decode it for us in the following format:
```
WH47 H47H 90D W20U9H7
```

Between spaces we need to add the underscore character, and wrap it between picoCTF{}. We'll find the flag:
```
picoCTF{wh47_h47h_90d_w20u9h7}
```

-----------------------------------------------------------------------------------


