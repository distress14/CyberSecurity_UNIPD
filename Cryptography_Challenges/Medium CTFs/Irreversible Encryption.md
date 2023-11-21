
You are given this Python Script:
```Python
#!/usr/bin/env python3

import base64
import string
import binascii

ALPHABET = list(string.printable) # len = 100
LEN = len(ALPHABET)
FLAG = "??????????????????????????????????????????????"

# b64 encoding is safe and my flag secure
def base64encode(message):
	message_bytes = message.encode('ascii')
	b64_bytes = base64.b64encode(message_bytes)
	b64_message = b64_bytes.decode('ascii')
	return b64_message

# same for b32
def base32encode(message):
	message_bytes = message.encode('ascii')
	b32_bytes = base64.b32encode(message_bytes)
	b32_message = b32_bytes.decode('ascii')
	return b32_message

# I think I'm forgetting something important to remove here
def XORencode(message, KEY="c4mPar1"):
	rep = len(message)//len(KEY) + 1
	key = (KEY*rep)[:len(message)] # adjust the key len
	xored = ''.join([chr(ord(a) ^ ord(b)) for a,b in zip(message, key)])
	return xored

# Easy-to-use function, that looks useful
def ROTencode(message, pos):
	rot13_enc = ''
	for c in message:
		i = ALPHABET.index(c)
		rot13_enc += ALPHABET[(i+pos)%LEN]
		return rot13_enc

# a useless method that could be replaced by a single line of code
# why not?
def ascii_to_hex(message):
	encoded = binascii.hexlify(message).decode()
	return encoded

# do it 15 times plz
encrypted = "Encode as if there's no tomorrow: " + FLAG

[1]

for _ in range(15):
	# encode the FLAG in the 4 different ways, always the same order
	b64_encrypted = base64encode(encrypted)
	rot13_encrypted = ROTencode(b64_encrypted, 13)
	b32_encrypted = base32encode(rot13_encrypted)
	encrypted = ROTencode(b32_encrypted, 3)

[2]

# I was told that XOR is a secure operation
xor_encrypted = XORencode(encrypted).encode('ascii')

[3]

# hopefully also the hex encoding will strengthen the encryption operation
hex_encrypted = ascii_to_hex(xor_encrypted)

[4]

# save the result for later use
# none will decrypt it anyway
with open("encrypted_flag.txt", "w") as f:   #or Irreversible Encryption-encrypted_flag.txt
	f.write(hex_encrypted)
	f.close()
```

I need to find a way to reverse these operations. Added [number] to identify the steps

As a first step, I rename the variables in the for loop [1] and reorder, in reverse, the steps used

From:
```Python
for _ in range(15):
	# encode the FLAG in the 4 different ways, always the same order
	b64_encrypted = base64encode(encrypted)
	rot13_encrypted = ROTencode(b64_encrypted, 13)
	b32_encrypted = base32encode(rot13_encrypted)
	encrypted = ROTencode(b32_encrypted, 3)
```
To:

```Python
for _ in range(15):
	decoded = ROTencode(decoded, 3)
	decoded = base32encode(decoded)
	decoded = ROTencode(decoded, 13)
	decoded = base64encode(decoded)
	# encode the FLAG in the 4 different ways, always the same order
```

Let's focus on the ROTencode function, (ROT=rotation) you have to change the pos from positive (+3) to negative (-3), when it is called in the for loop, by reversing its encryption. You must not change ANYTHING within the ROTencode function.

```Python
def ROTencode(message, pos):
	rot13_enc = ''
	for c in message:
		i = ALPHABET.index(c)
		rot13_enc += ALPHABET[(i+pos)%LEN]
		return rot13_enc

decoded = ROTencode(decoded, -3)
```

Now let's focus on the base32encode function (That's not the base64.b32encode from Base64 lib! )
```Python
def base32encode(message):
	message_bytes = message.encode('ascii')
	b32_bytes = base64.b32encode(message_bytes)        #Change it here
	b32_message = b32_bytes.decode('ascii')
	return b32_message
```
You must not change ANYTHING within the base32encode function, except for:

From:
```Python
b32_bytes = base64.b32encode(message_bytes)
```

To:
```Python
b32_bytes = base64.b32decode(message_bytes)
```

Do the exact same thing for the function base64encode.

Now we need to reverse the XORencode function [2] :
```Python
xor_encrypted = XORencode(encrypted).encode('ascii')
```

For the properties of the XOR, there is no need to change anything in the function. But before that, we need to decode it separately into ascii:
```Python
decoded = decoded.decode('ascii')
decoded = XORencode(decoded)
```

Let us analyze the ascii_to_hex function. We note that only one line of code is used, so we can directly write it out of the function, saving memory and time
```Python
hex_encrypted = ascii_to_hex(xor_encrypted)
```
```Python
def ascii_to_hex(message):
	encoded = binascii.hexlify(message).decode()
	return encoded
```

We can rewrite it as follows
```Python
decoded = binascii.unhexlify(hex_encrypted)
```

I used hex_encrypted instead of decoded because in reverse, the last function saves to hex_encrypted, so I keep it the same:
```python
with open("encrypted_flag.txt", "w") as f:   #or Irreversible Encryption-encrypted_flag.txt
	f.write(hex_encrypted)
	f.close()
```

Now if we reorder the function/steps [1]  [2]  [3]  [4] to  [4]  [3]  [2]  [1] we'll have:

```Python
# Ex[4]
# open the file and read the flag
with open("encrypted_flag.txt", "r") as f:
	hex_encrypted = f.read()
	f.close()

# Ex[3]
# hopefully also the hex encoding will strengthen the encryption operation
decoded = binascii.unhexlify(hex_encrypted)
decoded = decoded.decode('ascii')

# Ex[2]
# I was told that XOR is a secure operation
decoded = XORencode(decoded)

# Ex[1]
for _ in range(15):
	# encode the FLAG in the 4 different ways, always the same order
	decoded = ROTencode(decoded, -3)
	decoded = base32encode(decoded)
	decoded = ROTencode(decoded, -13)
	decoded = base64encode(decoded)

print(f'[!] The message is = {decoded}')
```
Output: 
The message is = Encode as if there's no tomorrow: spritz{But_wa1t_R3vers1ble_OP3rations_are_B4D}

Ps. Remember to save/use the functions ROTencode, base32encode, base64encode.


