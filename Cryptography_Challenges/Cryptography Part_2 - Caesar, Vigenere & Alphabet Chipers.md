## Challenge 4.1 - Julius (Caesar Chiper)

[For Mac/Win/Linux System]
#### Description :
```
Julius,Q2Flc2FyCg==
-------------------
World of Cryptography is like that Unsolved Rubik's Cube, given to a child that has no idea about it. A new combination at every turn.
Can you solve this one, with weird name?

ciphertext: fYZ7ipGIjFtsXpNLbHdPbXdaam1PS1c5lQ==

```
IT: L'obbiettivo di questa CTF è di usare il cifrario di cesare per decriptare il cipher text e trovare la Flag

ENG: The goal of this CTF is to use Caesar's cipher to decrypt the cipher text and find the Flag

#### Solution :
```Python
#in the first line of the description contains an hint
# Julius,Q2Flc2FyCg==

# since it ends with ==, the first hypothesis is
#that this is a base64 encoding
#let's decodi it!
import base64
enc_b64 = 'Q2Flc2FyCg=='

#we define a function. It might be helpful in future
def base64tostring(text):
	return base64.b64decode(text).decode('utf-8', errors="ignore")

print(f"Decoding=\t{base64tostring(enc_b64)}")

#the hints says "caesar", and we know a famous cipher
#with this name. We can apply e reverse to the
# ciphered text given in description
puzzle = 'fYZ7ipGIjFtsXpNLbHdPbXdaam1PS1c5lQ=='
print("The length of the puzzle is:\t", len(puzzle))

# the length is a multiple of 4, and the alphabet seems too regular (no punctuation).
#we can think that this is a base64 encoded string
puzzle_dec = base64tostring(puzzle)
print("Decoded puzzle:", puzzle_dec)

# now we have a lot of no sense characters. We can try to apply
# the ceasar cipher
def ceasar_cracker(text, from_ = -30, to_=+30):
	for i in range(from_, to_): #possible keys [-30, 30]
		#decode
		curr_step = ''.join([chr(ord(c) + i) for c in text])
		#print
		print(f"Step={i}\t{curr_step}")

ceasar_cracker(puzzle_dec)
## we look for some readable flags. We find one at step -24
```
IT: Scriviamo una funzione che decifri per noi grazie al cifrario di Cesare. Tornerà utile per i prossimi esercizi

ENG: We write a function that deciphers for us thanks to Caesar's cipher. It will come in handy for future exercises

```Python
def ceasar_cracker(text, from_ = -30, to_=+30):
	for i in range(from_, to_): #possible keys [-30, 30]
		#decode
		curr_step = ''.join([chr(ord(c) + i) for c in text])
		#print
		print(f"Step={i}\t{curr_step}")
```
IT: Eseguito il Caesar cracker, verrà stampata la nostra flag= {ecCTF3T_7U_BRU73?!}, ottenuta shiftando -24 volte 

ENG: Running the Caesar cracker will print our flag= {ecCTF3T_7U_BRU73?!}, obtained by shifting -24 times

-----------------------------------------------------------------------------------

## Challenge 4.2 - I agree (Vigenere Chiper)

[For Mac/Win/Linux System]
#### Description :
```
Crack the cipher: vhixoieemksktorywzvhxzijqni
Your clue is:

"caesar is everything. But he took it to the next level."
```
IT: L'obbiettivo di questa CTF è di usare il cifrario di cesare (o una sua versione "migliore") per decriptare il cipher text e trovare la Flag. 

ENG: The goal of this CTF is to use the Caesar cipher (or a "better" version of it) to decrypt the cipher text and find the Flag. 

#### Solution :
```Python
# The description says:
# "ceasar is everything"

#maybe it is a ceasar cipher, and we need to
#crack it as in the previous exercise
puzzle = 'vhixoieemksktorywzvhxzijqni'

def ceasar_cracker(text, from_ = -30, to_=+30):
	for i in range(from_, to_): #possible keys [-30, 30]
		#decode
		curr_step = ''.join([chr(ord(c) + i) for c in text])
		#print
		print(f"Step={i}\t{curr_step}")

ceasar_cracker(puzzle)

# I don't see any proper flag. We need to find another way
# The description says that it is the "next level" of ceasar.

# After some investigation, we can find that the evolution
# of a ceasar cipher is the vigenere cipher.

#However, the vigenere requires also a key.
# Google can help us! There are some online bruteforce services
#for these kind of ciphers.

#https://www.guballa.de/vigenere-solver

# the flag is reached: theforceisstrongwiththisone
# the key is "ceasar" ... as the hint suggested
```

L'evoluzione del Caesar Cipher è il Vigenere Cipher, controlla:
```
https://www.guballa.de/vigenere-solver
```

-----------------------------------------------------------------------------------

## Challenge 4.3 - Alphabet soup (Alphabet Cipher)

[For Mac/Win/Linux System]

#### Description :
```
MKXU IDKMI DM BDASKMI NLU XCPJNDICFQ! K VDMGUC KW PDT GKG NLKB HP LFMG DC TBUG PDTC CUBDTCXUB. K'Q BTCU MDV PDT VFMN F WAFI BD LUCU KN KB WAFI GDKMINLKBHPLFMGKBQDCUWTMNLFMFMDMAKMUNDDA
```
IT: L'obbiettivo di questa CTF è di trovare la Flag facendo CryptoAnalisi, cercando (e/o indovinando) quali lettere rappresentano quelle vere.

ENG: The goal of this CTF is to find the Flag by doing Cryptoanalysis, looking for (and/or guessing) which letters represent the real ones.

#### Solution :
```Python
#we only have an encrypted message

puzzle = "MKXU IDKMI DM BDASKMI NLU XCPJNDICFQ! K VDMGUC KW PDT GKG NLKB HP LFMG DC TBUG PDTC CUBDTCXUB. K'Q BTCU MDV PDT VFMN F WAFI BD LUCU KN KB WAFI GDKMINLKBHPLFMGKBQDCUWTMNLFMFMDMAKMUNDDA"

#since I do not have any clue, I try to use the cryptanalysis strategy
#in the ciphers, in general, each letter is associated to a given alphabet
# we can try to find possible associations.
#the first step is to see the frequency of each characters
chr2freq = {}

for c in puzzle:
	if c not in chr2freq:
		chr2freq[c] = 1
	else:
		chr2freq[c] += 1

sorted_x = sorted(chr2freq.items(), key=lambda kv: kv[1], reverse = True)
#https://stackoverflow.com/questions/8966538/syntax-behind-sortedkey-lambda
print(sorted_x)

# hypothesis 1: the text is english written
# we can find online what are the most used english characters
# e.g., http://pi.math.cornell.edu/~mec/2003-2004/cryptography/subs/frequencies.html

# we see that the 'K' is "alone", and we can think to
# K = I
voc = {'K': 'i'}
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#then there is an 'i'Q', which is likely an M
voc['Q'] = 'm'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#F -> 'a'
voc['F'] = 'a'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

## the semilast word contains four letters, and the third character
# is an 'a'. This word could be flag
voc['W'] = 'f'
voc['A'] = 'l'
voc['I'] = 'g'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#not a lot of info...
#however, there is a word with GiG ... G must be a 'D'
voc['G'] = 'd'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#then there is a sentence with "if PDT did"
# PDT could be "you", a likely word with letters not used yet
voc['P'] = 'y'
voc['D'] = 'o'
voc['T'] = 'u'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#slightly better. The second word is goiMg
# M->n
voc['M'] = 'n'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#back on the second sentence
# if you did NLiB Hy ... seems "if you did this by"
voc['N'] = 't'
voc['L'] = 'h'
voc['B'] = 's'
voc['H'] = 'b'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#the fourth word must be "solving"
voc['S'] = 'v'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#fifth word is the
voc['U'] = 'e'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#then, "I wonder if you ..."
voc['V'] = 'w'
voc['C'] = 'r'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#ready to conclude. we can see the flag .. but lets finish the job

#niXe -> nice
voc['X'] = 'c'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

#the last word of the fist sentence is cryptogram
voc['J'] = 'p'
dec = ''.join(c if c not in voc else voc[c] for c in puzzle)

print(voc, '\n' ,dec)

## we did it

# nice going on solving the cryptogram!
#i wonder if you did this by hand or used your resources.
```
We have reached our Flag = {doingthisbyhandismorefunthananonlinetool}

-----------------------------------------------------------------------------------

## Challenge 4.4 - Simpledes (Cryptoanalysis & Reverse Introduction)

[For Mac/Win/Linux System]
#### Description :
```
Larry is working on an encryption algorithm based on DES.
He hasn't worked out all the kinks yet, but he thinks it works.
Your job is to confirm that you can decrypt a message, given the algorithm and parameters used.

His system works as follows:

	1. Choose a plaintext that is divisible into 12bit 'blocks'
	2. Choose a key at least 8bits in length
	3. For each block from i=0 while i<N perform the following operations
	4. Repeat the following operations on block i, from r=0 while r<R
	5. Divide the block into 2 6bit sections Lr,Rr
	6. Using Rr, "expand" the value from 6bits to 8bits.
		Do this by remapping the values using their index, e.g.
		1 2 3 4 5 6 -> 1 2 4 3 4 3 5 6
	7. XOR the result of this with 8bits of the Key beginning with Key[iR+r] and wrapping back to the beginning if necessary.
	8. Divide the result into 2 4bit sections S1, S2
	9. Calculate the 2 3bit values using the two "S boxes" below, using S1 and S2 as input respectively.

	S1	0	1	2	3	4	5	6	7
	0	101	010	001	110	011	100	111	000
	1	001	100	110	010	000	111	101	011
	
	S2	0	1	2	3	4	5	6	7
	0	100	000	110	101	111	001	011	010
	1	101	011	000	111	110	010	001	100
	
	10. Concatenate the results of the S-boxes into 1 6bit value
	11. XOR the result with Lr
	12. Use Rr as Lr and your altered Rr (result of previous step) as Rr for any further computation on block i
	13. increment r
	
	
He has encryped a message using Key="Mu", and R=2. See if you can decipher it into plaintext.
Submit your result to Larry in the format Gigem{plaintext}.

Binary of ciphertext: 01100101 00100010 10001100 01011000 00010001 10000101
```
IT: L'obbiettivo di questa CTF è di trovare la Flag, provando a fare un inizio di reverse engineering

ENG: The goal of this CTF is to find the Flag, trying to make a beginning of reverse engineering

#### Solution :
```Python
#the description give us a simplified version of DES.
#the first idea is to reconstruct the process

#Rule13 increment r
def rule9b0(b):
	#get indexed
	row = int(b[0])
	col = int(b[1:], 2)

	matrix = [['101','010', '001', '110', '011', '100', '111', '000'],
			['001', '100', '110', '010', '000','111', '101', '011']]
	return matrix[row][col]

def rule9b1(b):
	#get indexed
	row = int(b[0])
	col = int(b[1:], 2)
	
	matrix = [['100','000','110','101','111','001','011','010'],
			['101','011','000','111','110','010','001','100']]
	return matrix[row][col]

# we need to convert the text into bits
def string2binary(text):
	return ''.join(f"{ord(c):08b}" for c in text)

def binary2string(text):
	return ''.join(f"{ord(c):08b}" for c in text)

def splitblock(block):
	Lr = block[:6]
	Rr = block[6:]
	return Lr, Rr

def expand_miniblock(b):
	return b[0] + b[1] + b[3] + b[2] + b[3] + b[2] + b[4] + b[5]

def xor(a, b):
	res = int(a, 2) ^ int(b, 2)
	return f"{res:08b}"

def encrypt(text, key, R):
	text_encr = ''

#Rule 1.
text_bin = string2binary(text)
if (len(text_bin) % 12 != 0):
	raise Exception(f'Rule 1 not respected.')

#Rule 2
key_bin = string2binary(key)
if (len(text_bin) < 8):
	raise Exception('Rule 2 not respected')

#rule3
#we have some blocks ...
for bnum in range(len(text_bin) // 12):
	i = bnum

#define the block
from_ = 0 + 12*bnum
to_ = 12 * (bnum + 1)
block = text_bin[from_:to_]

#rule4
for r in range(R):
	#rule5
	Lr, Rr = splitblock(block)

#rule6
Rr_expanded = expand_miniblock(Rr)

#Rule7
curr_key = key_bin[(i* R + r) : ((i* R + r)+8)]
Rr_exp_xor_key = xor(Rr_expanded, curr_key)

#Rule8
Rr_exp_xor_key_0 = Rr_exp_xor_key[:4]
Rr_exp_xor_key_1 = Rr_exp_xor_key[4:]

#Rule9
Rr_exp_xor_key_0_conv = rule9b0(Rr_exp_xor_key_0)
Rr_exp_xor_key_1_conv = rule9b1(Rr_exp_xor_key_1)

#Rule10
Rr_sboxes = Rr_exp_xor_key_0_conv + Rr_exp_xor_key_1_conv
if len(Rr_sboxes) != 6:
	raise Exception("Error on Rule 10")

#Rule11
Rr_alt = xor(Lr, Rr_sboxes)[2:]

#Rule12
block = Rr + Rr_alt

#Rule13
#end of step
#append the result.
text_encr += block
return text_encr

#solution
def decrypt(text, key, R):
	text_dec = ''

#the text is already in the bit format.
#we only need to convert the key
text_bin = text
key_bin = string2binary(key)

if (len(text_bin) < 8):
	raise Exception('Rule 2 not respected')

#similar to the previous cycle, we need to iterate over the blocks.
#since the blocks are independent between each other, we can use the
#same order of the encryption algorithm
for bnum in range(len(text_bin) // 12):
	i = bnum

#define the block
from_ = 0 + 12*bnum
to_ = 12 * (bnum + 1)
block = text_bin[from_:to_]

#we now need to reverse the rule4 loop
#since this time the results obtained in a specific round affect the
#next one, we use the reverse order
#our goal is to retrieve the original Lr and Rr

for r in range(R-1, -1, -1):
	#in the first round we obtain the components
	# block = Lr + Rr
	Rr, Rr_alt = splitblock(block)

#to reverse Rule11 we can use the xor properties
#e.g.: A xor B = C, C xor B = A
#however, we need to have one of the components at least (A or B) since
# we have C
# N.B. we actually have something useful. Which is Rr.
# We know half of the info! we can wasilt obtain Rr_sboxes
# compute from rule6 to rule10, where Lr is not involved at all

#rule6
Rr_expanded = expand_miniblock(Rr)

#Rule7
curr_key = key_bin[(i* R + r) : ((i* R + r)+8)]
Rr_exp_xor_key = xor(Rr_expanded, curr_key)

#Rule8
Rr_exp_xor_key_0 = Rr_exp_xor_key[:4]
Rr_exp_xor_key_1 = Rr_exp_xor_key[4:]

#Rule9
Rr_exp_xor_key_0_conv = rule9b0(Rr_exp_xor_key_0)
Rr_exp_xor_key_1_conv = rule9b1(Rr_exp_xor_key_1)
Rr_sboxes = Rr_exp_xor_key_0_conv + Rr_exp_xor_key_1_conv

#Rule10
if len(Rr_sboxes) != 6:
	raise Exception("Error on Rule 10")

#we can finally obtain Lr
Lr = xor(Rr_alt, Rr_sboxes)
Lr = Lr[2:]
block = Lr + Rr

#obtain the new block
new_block = Lr + Rr
#print(new_block)

# raise Exception('# DEBUG: ')

#append the result.
text_dec += new_block

#Convert from 8digit bits into the integer, and then
#in the ascii representation
res = ''
for i in range(len(text_dec) // 8):
	res += chr(int(text_dec[(i * 8): ((i+1) * 8)] ,2))

print(res)

#print(encrypt('abc', 'Mu', 2))
puzzle = "011001010010001010001100010110000001000110000101"
key_ex = 'Mu'
R_ex = 2

#decrypt(puzzle, key_ex, R_ex)
decrypt(encrypt('Min0n!', 'Mu', 2), 'Mu', 2)
```
We obtained the Flag = {Min0n!}


[Cryptography Part_3 - Hash Cracking - XOR - Algorithm Cryptoanalysis](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_3%20-%20Hash%20Cracking%20-%20XOR%20-%20Algorithm%20Cryptoanalysis)

[Cryptography Part_1 - Book cipher - XOR - Base642ASCII](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_1%20-%20Book%20cipher%20-%20XOR%20-%20Base642ASCII)
