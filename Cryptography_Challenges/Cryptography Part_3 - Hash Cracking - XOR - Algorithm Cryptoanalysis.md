## Challenge 5.1 - Crack The Hash (Hash Cracking)

[For Mac/Win/Linux System]
#### Description :
```
It’s happened again! Some of our beloved friends at linkedin.com forgot to salt their password hashes. Due to a rather interesting SQL injection issue, a hacker group has published the following MD5 hash online! Can you crack it?

Hash: 365d38c60c4e98ca5ca6dbc02d396e53

Hint. Use a md5 cracker
```
IT: Obbiettivo di questa CTF è di trovare la Flag partendo da un Hash fornito

ENG: The goal of this CTF is to find the Flag starting from a provided Hash

#### Solution :
```
We have the following MD5 hash:
365d38c60c4e98ca5ca6dbc02d396e53

The description suggests us to use a tool.
https://crackstation.net/

the password is password12345
```
IT: asta semplicemente cercare un hash cracker online, darli in input l'hash fornito e premere invio. 
Verrà fornita la password in chiaro.

ENG: Simply search for a hash cracker online, give them as input the hash provided and press enter. 
The password in plain text will be provided.

-----------------------------------------------------------------------------------
## Challenge 5.2 - ReadyXorNot (XOR)

[For Mac/Win/Linux System]
### Description :
```
original data: "El Psy Congroo"
encrypted data: "IFhiPhZNYi0KWiUcCls="
encrypted flag: "I3gDKVh1Lh4EVyMDBFo="

The flag is a composition of two names (two animals (?)).
```
IT: Obbiettivo di questa CTF è di decriptare la Flag fornita

ENG: The objective of this CTF is to decrypt the Flag provided

IT ------------------------------------------------------------------------------------------
Suggerimento 1: Possiamo notare che le stringhe sono state criptate in base64 (notare = alla fine della stringa) e che ogni stringa ha la stessa lunghezza. Dato il nome della challenge (XOR), ci viene suggerito di sfruttare appunto l'operazione XOR

Suggerimento 2: Per completare la CTF e ottenere la Flag, bisogna decriptare le stringhe 
Siccome abbiamo sia il testo in chiaro che la sua controparte criptate, possiamo sfruttare la XOR per trovare la chiave. Notare che bisogna prima convertire i caratteri della stringa in valori ASCII, effettuare la XOR e riconvertirli in caratteri ASCII.

ENG ----------------------------------------------------------------------------------------

Hint 1: We can see that the strings have been encrypted in base64 (note = at the end of the string) and that each string has the same length. Given the name of the challenge (XOR), we are suggested to exploit precisely the XOR operation  
  
Hint 2: To complete the CTF and get the Flag, we need to decrypt the strings.   
Since we have both the plaintext and its encrypted counterpart, we can exploit XOR to find the key. Note that we must first convert the characters in the string to ASCII values, perform the XOR and convert them back to ASCII characters.

#### Solution :
```Python
import base64

original_data = "El Psy Congroo"
encrypted_data = "IFhiPhZNYi0KWiUcCls="
encrypted_flag = "I3gDKVh1Lh4EVyMDBFo="

#we can note that all of the strings have the same lenght
#since we have an example of encryption, and we know that this is a xor,
#we can simply try to obtain the key in the example, and apply it to the
#crypted flag
def base64tostring(text):
return base64.b64decode(text).decode('utf-8', errors="ignore")

#decode the encryption from base64
enc_data= base64tostring(encrypted_data)
enc_flag= base64tostring(encrypted_flag)

#we now apply the xor to obtain the key
key = ''.join([chr(ord(x) ^ ord(y))for x, y in zip(original_data, enc_data)])
print('key:\t',key)

#this seems a reasonalble key
flag = ''.join([chr(ord(x) ^ ord(y))for x, y in zip(enc_flag, key)])

print("Flag:\t", flag)
```
Flag found = Alpacaman

-----------------------------------------------------------------------------------

## Challenge 5.3 - TOP (Algorithm Cryptoanalysis)

[For Mac/Win/Linux System]
#### Description :
```
Perfectly secure. That's for sure! Or can break it and reveal my secret?
We are given a encryption script and the a file which is encrypted with it
```
IT: e cerchiamo di aprire il file top_secret, ci verrà mostrato questa stringa (senza senso)

ENG: If we try to open the top_secret file, we will be shown this (meaningless) string

```
f∏ù,π⁄fúXÇ^ﬂ˜î qDµ8{ªtI±yÜïVu≥ﬁ[ùH∞ ≈Ü˝„" øÙ¥oVé•©óπΩπªøπ±πªª¶∞ø∫∞øΩ∫
```

#### Script provided:
```Python
#!/usr/bin/env python3
import random
import sys
import time

cur_time = str(time.time()).encode('ASCII')
random.seed(cur_time)

msg = input('Your message: ').encode('ASCII')
key = [random.randrange(256) for _ in msg]
c = [m ^ k for (m,k ) in zip(msg + cur_time, key + [0x88]*len(cur_time))]

with open(sys.argv[1], "wb") as f:
	f.write(bytes(c))
```

#### Solution :
```Python
#to solve this challenge, we can try to find some weaknesses in the
#given algoruthm
#we can debug it
import random
import sys
import time

# =============================================================================
# step 1 - set seed
# =============================================================================

cur_time = str(time.time()).encode('ASCII')
random.seed(cur_time)
print('Step 1- current time:\t', cur_time)

#note1: current time is a byte value containing a number, which will set a seed
#floating value

# =============================================================================
# step 2 - get message
# =============================================================================
msg = 'hello'.encode('ASCII')

# =============================================================================
# step 3 - define the key
# =============================================================================

key = [random.randrange(256) for _ in msg]
#the key is a list of values = len(len of messages)
# one value for each character in the message

# =============================================================================
# step 4 - encryption
# =============================================================================

c = [m ^ k for (m,k ) in zip(msg + cur_time, key + [0x88]*len(cur_time))]

#the encryption is composed by a xor between a character and a key.
#the message is the concatenation of msg + cur_time
#the key is the concatenation of the list of keys + list of 0x88

####--------RESOLUTION -----------------
#we know that |msg| = |key|, and |cur_time| = |[0x88]|
#we can use the xor property to retrieve the cur_time of the execution

#read the secret
with open("top_secret", "rb") as f:
	secret = f.read()
print(len(secret))

#extract the encrypted current time
sec_time = secret[-len(cur_time):]
plain_time = ''.join([chr(m ^ k) for (m, k) in zip(sec_time, [0x88]*len(cur_time))])
print(f"plain time:\t{plain_time}")
#what we printed seems a correct datatime format

#we now leverage on the pseudonumber vulnerabilities ...
#the algorithm set a seed, so it is not random the generator.
random.seed(plain_time.encode("ASCII"))

#get the keys
keys_secret = [random.randrange(256) for _ in secret[:-len(cur_time)]]
plain_text = ''.join([chr(m ^ k) for (m, k) in zip(secret[:-len(cur_time)], keys_secret)])

print(plain_text)

#flag reached
```
We got the flag = {34C3_otp_top_pto_pot_tpo_opt_wh0_car3s}


Next => [Cryptography Part_4 - User Authentication (HTTP.TCP.EncryptedTCP)](<obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_4%20-%20User%20Authentication%20(HTTP.TCP.EncryptedTCP)>)

Previous => [Cryptography Part_2 - Caesar, Vigenere & Alphabet Chipers](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_2%20-%20Caesar%2C%20Vigenere%20%26%20Alphabet%20Chipers)

