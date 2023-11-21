## Challenge 3.1 - Book Cipher

[For Mac/Win/Linux System]

Description:
```
The hard drive may be corrupted, but you were able to recover a small chunk of text (see "book.txt").
Scribbled on the back of the hard drive is a set of mysterious numbers. Can you discover the meaning behind these numbers? (1, 9, 4) (4, 2, 8) (4, 8, 3) (7, 1, 5) (8, 10, 1)
```

IT: L'obbiettivo di questa CTF è di decifrare una porzione di testo (book.txt) usando gli indizi dati
ENG: The goal of this CTF is to decipher a portion of text (book.txt) using the clues given

Book:
```
It might have been expected that the attempt to trace to their origin
in the past the institutions and customs in common use upon the sea
would from an early date occupy the attention of a seafaring people,
but for some obscure reason the British nation has always been
indifferent to the history of its activities upon that element on which
its greatness was founded, and to which it has become more and more
dependent for its daily bread and its very existence. To those who
are alive to this fact it will hardly come as a surprise, therefore,
to learn that the first sustained attempt at a detailed investigation
into the history of the flag at sea was made under the patronage
of the German Admiralty by a German Admiral. Vice-Admiral Siegel's
_Die Flagge_, published in 1912, was the first book to deal with the
development of the flag at sea in a scientific spirit, and although
the earlier chapters contain some mistakes due to his employment of
translations of early works instead of original texts, and the accounts
of the British flags in the later chapters suffer because he had no
access to original records, it is a worthy piece of work.

The present book is an attempt to remove the reproach to the British
nation which this implies. Its plan is somewhat different from that
of the work referred to above. Instead of dealing with the flags of
all maritime nations of the world--a task that (if it was to be more
than a mere copying or compilation) would entail much work in foreign
archives--it seemed more profitable to concentrate upon the history
of British Naval Flags, for researches made so far back as 1908 had
taught me how much that is inaccurate about their history had received
acceptance. But first it seemed necessary to devote some time and
space to the inquiry into the origin of the flag and how it became the
honoured symbol of nationality that it now is, and for this a general
view had to be taken in order that a firm foundation might be laid for
the early history of our own flags.

In the first chapter the ground worked over by Admiral Siegel has been
solidified by examination of the original authorities, with the result
that a few errors have been detected and some new facts brought to
light, and the investigation has also been extended further; the most
important of the additions being those relating to the standards in
the Phoenician and Greek ships of war, forms of the early "standard"
and "gonfanon," and the Genoese Standard of St George and the Dragon.
For the deduction that the use of a national flag arose in the Italian
city states I take the entire responsibility, well aware that further
investigations may possibly bring to light fresh facts which will
overthrow it.

The chapter on early English, Scottish and Irish flags serves as an
introduction to the history of our national flag, which was invented
for the use of the mercantile marine, though it was very soon
appropriated by the Royal Navy for its sole use. It is very improbable
that further research will enable the gap left by the unfortunate
destruction of the early 17th century records to be filled, so that the
story of the Union Flag may be taken as being substantially complete,
but there is still room for further work upon the history of its
component crosses. It will be seen that I have been unable to find any
solid ground for the common belief that the cross of St George was
introduced as the national emblem of England by Richard I, and am of
opinion that it did not begin to attain that position until the first
years of the reign of Edward I.

The chapters on the flags used to indicate distinctions of command and
service at sea give an account of the use (now obsolete) of the Royal
Standard at sea by naval commanders-in-chief; of the history of the
Admiralty anchor-flag; and of the steps by which the present Admirals'
flags were evolved. The history of the ensigns from their first
adoption at sea about the end of Elizabeth's reign has been set out in
some detail, but further research may bring to light more details of
interest in the years between 1574 and 1653. The causes which led to
the adoption of a red ensign as the most important British ensign and
the steps which led to its appropriation to the Mercantile Marine, and
not the Royal Navy, are stated as far as the records availed, though
here again further research is needed in the late Elizabethan and
early Stuart periods among records that may still survive in private
ownership. These chapters may, perhaps, appeal rather to the seaman
and the student of naval history than to the general reader, but it is
hoped that they may also prove of service to artists who wish to avoid
the anachronisms into which some of their brethren have been betrayed.

In order that the development of flag signals may be properly
appreciated it has been necessary, when dealing with the earlier years,
to take into account what had happened outside the narrow circuit of
British waters. The earlier matter, though here examined solely from
the point of view of the flags used, offers considerable interest to
the student of naval tactics, with which indeed the art of signalling
is inseparably connected.

The last chapter, on Ceremonial and other usages, is, from the author's
point of view, the least satisfactory. From the nature of the subject,
the official records contain very little information about it. It
is only by the slow and laborious process of examining contemporary
journals, diaries, accounts of voyages, and similar material that facts
can be found for any exhaustive treatment of these matters. Something
of this has been done, but more remains to do.

In concluding the work which has occupied a large portion of the
leisure hours of many years, it is my pleasant duty to express my
gratitude to the numerous friends whose encouragement and assistance
have enabled me to persevere in what has proved a somewhat arduous
task; especially to Sir Julian Corbett, who has read the proofs and
given me the benefit of his criticisms; to the officials of the
Pepysian Library, Public Record Office, British Museum and London
Library for the facilities afforded me; and not least to my friend Mr
Vaughan who has spared no pains in the preparation of the coloured
plates.
```

Solution:
```
Gli indizi rimandano a questo: 
(1, 9, 4) = (paragrafo, linea, parola)
La prima parola si trova nel primo paragrafo, alla nona linea e dopo 4 parole dall'inizio della linea

Basta semplicemente cercare ogni parola e unirle alla fine in un'unica frase:

(1, 9, 4) === the
(4, 2, 8) === flag 
(4, 8, 3) === is  
(7, 1, 5) === Ceremonial
(8, 10, 1) === plates
```

The flag is: "The flag is Ceremonial plates."

-----------------------------------------------------------------------------------

## Challenge 3.2 - Sherlock

[For Mac/Win/Linux System]

Description:
```
Sherlock has a mystery in front of him. Help him to find the flag.
```

IT: L'obbiettivo di questa CTF è di trovare la flag nel file challenge.txt fornito
ENG: The goal of this CTF is to find the flag in the challenge.txt file provided

[challenge.txt](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCryptography_Challenges%2FChallenge_Sherlock) 

Solution:
```Python
#The first intui  is to notice that there are some characters uppercase, so we can open and filter them (we suggest to use Python).

#open the text file
with open('challenge.txt', 'r') as file:
    challenge = file.read()
    
#extract uppercase letters
insight=''.join([c for c in challenge if c.isupper()])
print(insight)

#The output is a string with a series of “ZERO” and “ONE”. We can first convert them into their numerical representation. 
insight = insight.replace('ZERO', '0')
insight = insight.replace('ONE', '1')

#We can then look of the length of this new string: it is a multiple of 8. The new intuition is that this string represents a series of unicode characters written I binary. We just need to reverse this process.

result=''.join(chr(int(insight[i*8:i*8+8],2)) for i in range(len(insight)//8))
print(result)
#And the flag is reached: BITSCTF{h1d3_1n_pl41n_5173}
```

IT: Siccome si notano alcune lettere in stampatello, possiamo procedere nel seguente modo:
ENG: Since we notice some block letters, we can proceed as follows:

```Python
with open('challenge.txt', 'r') as file:
    challenge = file.read()
```

IT: Apriamo il file e lo leggiamo
ENG: We open the file and read it

```Python
output1 += chr(ord(input[i]) + key)
```

IT: Nell'output andiamo ad aggiungere la decodifica.
ENG: In the output we are going to add decoding.

The flag is reached: BITSCTF{h1d3_1n_pl41n_5173}

-----------------------------------------------

## Challenge 3.3 - Ultraencoded

[For Mac/Win/Linux System]

Description:
```
Fady didn't understand well the difference between encryption and encoding, so instead of encrypting some secret message to pass to his friend, he encoded it!

The flag should be in the format: ALEXCTF
```

zero_one document:
```
ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO

ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ZERO ZERO ZERO ONE ZERO ONE ONE ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ONE ZERO ONE ZERO ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ONE ZERO ONE ZERO ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ZERO ZERO ONE ONE ZERO ZERO ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ZERO ZERO ZERO ONE ZERO ONE ZERO ZERO ZERO ONE ZERO ZERO ONE ONE ONE ONE ZERO ONE ZERO ZERO ONE ONE ONE ONE ZERO ONE
```

Solution:
```Python
#We can start by opening the file and converting the string into their numerical format, as in the previous exercice. Note that here there are additional spaces to remove.

#open the file
with open('zero_one', 'r') as file:
    input = file.read()
    #print(input)

#replace the zeros and ones in the numerical representation
input = input.replace('ZERO', '0')
input = input.replace('ONE', '1')
input = input.replace(' ', '') #remove additional spaces

#remove the additional spaces 
input = input.strip()

# Following the steps of exercise two, we conver the string from the binary representation in the ascii.

result=''.join(chr(int(input[i*8:i*8+8],2)) for i in range(len(input)//8))

#We can see that there are some odd characters: it is the MORSE code. Look online and build a proper dicitonary (dict structure). The flag is obtained by converting the morse to the alphabetical representation:

#convert morse to string
decoded2 = ''.join(morse2alpha.get(i) for i in decoded.split())

print(decoded2)
```

At this point, decoded2 will be our flag: ALEXCTFTH15O1SO5UP3RO5ECR3TOTXT

Next => [Cryptography Part_2 - Caesar, Vigenere & Alphabet Chipers](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_2%20-%20Caesar%2C%20Vigenere%20%26%20Alphabet%20Chipers)
