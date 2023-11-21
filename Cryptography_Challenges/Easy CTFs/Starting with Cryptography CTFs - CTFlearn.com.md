
Taked from: https://ctflearn.com

-----------------------------------------------------------------------------------
## Character Encoding - Challenge 115

Description:
```
In the computing industry, standards are established to facilitate information interchanges among American coders. Unfortunately, I've made communication a little bit more difficult. Can you figure this one out? 41 42 43 54 46 7B 34 35 43 31 31 5F 31 35 5F 55 35 33 46 55 4C 7D
```

It seams that we can use the Hexadecimal decoder to find the flag

I used: https://www.duplichecker.com/hex-to-text.php to convert:

From:
```
41 42 43 54 46 7B 34 35 43 31 31 5F 31 35 5F 55 35 33 46 55 4C 7D
```

To:
```
A B C T F { 4 5 C 1 1 _ 1 5 _ U 5 3 F U L }
```

If we delete the spaces created, we find the flag:
```
ABCTF{45C11_15_U53FUL}
```

-----------------------------------------------------------------------------------
## Base 2 2 the 6 - Challenge 192

Description:
```
There are so many different ways of encoding and decoding information nowadays... One of them will work! Q1RGe0ZsYWdneVdhZ2d5UmFnZ3l9
```

It seams that we can use the Base64 decoder to find the flag:

I used: https://www.base64decode.org to convert:

From:
```
Q1RGe0ZsYWdneVdhZ2d5UmFnZ3l9
```

To:
```
CTF{FlaggyWaggyRaggy}
```


-----------------------------------------------------------------------------------
## Morse Code - Challenge 309

Description:
```
..-. .-.. .- --. ... .- -- ..- . .-.. -- --- .-. ... . .. ... -.-. --- --- .-.. -... -.-- - .... . .-- .- -.-- .. .-.. .. -.- . -.-. .... . . ...
```

This is pretty forward, we can use an online Morse decoder to find the flag: https://morsecode.world/international/translator.html

If we convert the description, we are rewarded with the flag:
```
FLAGSAMUELMORSEISCOOLBYTHEWAYILIKECHEES
```


-----------------------------------------------------------------------------------
## Reverse Polarity - Challenge 230

Description:
```
I got a new hard drive just to hold my flag, but I'm afraid that it rotted. What do I do? The only thing I could get off of it was this: 01000011010101000100011001111011010000100110100101110100010111110100011001101100011010010111000001110000011010010110111001111101
```

We can use an online Binary converter to find the flag: https://www.convertbinary.com/to-text/

If we convert:
```
01000011010101000100011001111011010000100110100101110100010111110100011001101100011010010111000001110000011010010110111001111101
```

We are rewarded with the flag:
```
CTF{Bit_Flippin}
```


-----------------------------------------------------------------------------------
## Hextraordinary 158

Description:
```
Meet ROXy, a coder obsessed with being exclusively the worlds best hacker. She specializes in short cryptic hard to decipher secret codes. The below hex values for example, she did something with them to generate a secret code, can you figure out what? Your answer should start with 0x.

0xc4115 0x4cf8
```

If we meet ROXy, we can thing that we can use some sort of XOR operation to find the flag. 

So, we can go to: https://xor.pw/# , where:
```
Input1 = 0xc4115
Input2 = 0x4cf8
```
Same as saying:
```
0xc4115 ^ 0x4cf8 = ??
```

The result will be:
```
0xc4115 ^ 0x4cf8 = c0ded
```

Like the description says "```Your answer should start with 0x```", so we add 0x before c0ded:
```
Flag = 0xc0ded
```

We have found the flag

-----------------------------------------------------------------------------------

## Vigenere Cipher - Challenge 305

Description:
```
The vignere cipher is a method of encrypting alphabetic text by using a series of interwoven Caesar ciphers based on the letters of a keyword.<br />

I’m not sure what this means, but it was left lying around: blorpy

gwox{RgqssihYspOntqpxs}
```

Like the title says, it seams that they used the vigenere cipher to encode the text.

So we try to decode it with an online vigenere decoder: https://www.dcode.fr/vigenere-cipher

Do not forget to add the KEY used to encode it: blorpy

As result, we are rewarded with the flag:
```
flag{CiphersAreAwesome}
```

-----------------------------------------------------------------------------------

## Substitution Cipher - Challenge 238

Description:
```
Someone gave me this, but I haven't the slightest idea as to what it says! https://mega.nz/#!iCBz2IIL!B7292dJSx1PGXoWhd9oFLk2g0NFqGApBaItI_2Gsp9w Figure it out for me, will ya?
```

If we follow the Mega link, we'll have some sort of encrypted text:
```
MIT YSAU OL OYGFSBDGRTKFEKBHMGCALSOQTMIOL. UTFTKAMTR ZB DAKQGX EIAOF GY MIT COQOHTROA HAUT GF EASXOF AFR IGZZTL. ZT CTKT SGFU, MIT YSACL GF A 2005 HKTLTFM MODTL MIAF LMADOFA GK A CTTQSB LWFRAB, RTETDZTK 21, 1989 1990, MIT RKTC TROMGKL CAL WHKGGMTR TXTKB CGKSR EAF ZT YGWFR MIT EGFMOFWTR MG CGKQ AM A YAOMIYWS KTHSOTL CITKT IGZZTL, LMBST AOD EASXOF, AMMAEQ ZGMI LORTL MG DAKQL, "CIAM RG EGFMKGSSOFU AF AEMWAS ZGAKR ZGVTL OF MIT HKTHAKTFML FADT, OL ODHWSLOXT KADHAUTL OF CIOEI ASCABL KTYTKTFETL MIT HALLCGKR, CIOEI DGFTB, AFR MITB IAR SOMMST YKGFM BAKR IOL YKWLMKAMTR EGSGK WFOJWT AZOSOMB COMI AFR OFROLHTFLAMT YGK MTAEI GMITK LMWROTL, AKT ACAKRL ZARUTL, HWZSOLITR ZTYGKT CTSS AL A YOKT UKGLL HSAFL CTKT GKOUOFASSB EIAKAEMTKL OF MIT LMKOH MG CIOEI LTTD MG OM CITF MTDHTKTR OF AFR IASSGCOFU MITB'KT LODHSB RKACOFU OF UOXTL GF" HKOFEOHAS LHOMMST ROLMGKM, KTARTKL EGDOEL AKT WLT, CAMMTKLGF MGGQ MCG 16-DGFMIL AYMTK KTLOLMAQTL A DGKT EKTAM RTAS MG EASXOF GYMTF IGZZTL MG ARDOML "LSODB, "ZWM OM'L FADTR A FOUIM GWM LIT OL HGOFM GY FGM LTTF IGZZTL MIT ZGGQL AM MIAM O KTDAOFOFU ZGGQ IADLMTK IWTB AKT AHHTAKAFET: RTETDZTK 6, 1995 DGD'L YKADTL GY EASXOF UOXTF A CAUGF, LGDTMODTL MIAM LG OM'L YAMITKT'L YADOSB FG EAFETSSAMOGFLIOH CAL HKTLTFML YKGD FGXTDZTK 21, 1985 SALM AHHTAK AZLTFET OF AFGMITKCOLT OM IAHHB MG KWF OM YGK MIOL RAR AL "A SOMMST MG MGSTKAMT EASXOF'L YADOSB RKACF ASDGLM EGDDTFRTR WH ZTOFU HTGHST OFLMAFET, UTM DAKKOTR ZB A RAFET EASXOF'L GWMSAFROLOFU MIT FTCLHAHTK GK MAZSGOR FTCLHAHTK ZWLOFTLL LIGC OL GF!" AFR LHKOFML GY EIOSRKTF'L RAR'L YKWLMKAMTR ZB MWKF IWDGK, CAL HWZSOE ROASGU MITKT'L FGM DWEI AL "'94 DGRTKFOLD" CAMMTKLGF IAL RTSOUIML GY YAFMALB SOYT CAMMTKLGF LABL LTKXTL AL AF AKMOLML OL RTLMKWEMOGF ZWLOFTLL, LHAETYAKTK GY MIT GHHGKMWFOMOTL BGW ZGMI A MGHOE YGK IOL IGDT MGFUWT-OF-EITTQ HGHWSAK MIAM OM CAL "IGF" AFR JWAKMTK HAUT DGKT LHAEOGWL EAFETSSAMOGF MIT HAOK AKT ESTAKSB OF HLBEIOE MKAFLDGUKOYOTK'L "NAH" LGWFR TYYTEM BGW MIOFQTK CAMMTKLGF ASLG UKTC OFEKTROZST LHAET ZWBL OF EGDDGFSB CIOST GMITKCOLT OM'L FADT OL FGMAZST LMGKBSOFT UAXT MIT GHHGKMWFOMOTL BGW EAFETSSAMOGF MIT "EASXOF GYYTK MG DAQT IOD OFEGKKTEM AFLCTKL CAMMTK AKMCGKQ GMITK GYMTF CIOEI OL TXORTFM MG GMITK LMKOH OL MG MITOK WLT GY KWSTL MIAM LIGCF GF LAFROYTK, CIG WLTL A EKGCJWOSS ZT LTTF "USWTR" MG MIT GFSB HTKL AFR IOL YAMITK LWHHGKM OL SWFEISOFT UAXT MITLT MIOF A BTAK OF DWSMODAMTKOAS AFR GZMAOF GF LAFMALB, IOL WLT, CAMMTKL ROASGUWT OL AF "AKMOLM'L LMAMWL AL "A ROD XOTC OF MIT TLLTFMOASSB MG DAQT IOD LTTD MG OFESWRTR MIAM EASXOF OL AF GRR ROASGUWT DGLM GY MIT ESWZ IAL TVHKTLLOGF GWMLORT AXAOSAZST MG
```

Like the title says, we can imagine that they used some sort of substitution cipher to encode it;

So, if we go to:  https://planetcalc.com/8047/, we can try to bruteforce it and decode it:
```
THE FLAG IS IFONLYMODERNCRYPTOWASLIKETHIS. GENERATED BY MARKOV CHAIN OF THE WIKIPEDIA PAGE ON CALVIN AND HOBBES. BE WERE LONG, THE FLAWS ON A 2005 PRESENT TIMES THAN STAMINA OR A WEEKLY SUNDAY, DECEMBER 21, 1989 1990, THE DREW EDITORS WAS UPROOTED EVERY WORLD CAN BE FOUND THE CONTINUED TO WORK AT A FAITHFUL REPLIES WHERE HOBBES, STYLE AIM CALVIN, ATTACK BOTH SIDES TO MARKS, "WHAT DO CONTROLLING AN ACTUAL BOARD BOXES IN THE PREPARENTS NAME, IS IMPULSIVE RAMPAGES IN WHICH ALWAYS REFERENCES THE PASSWORD, WHICH MONEY, AND THEY HAD LITTLE FRONT YARD HIS FRUSTRATED COLOR UNIQUE ABILITY WITH AND INDISPENSATE FOR TEACH OTHER STUDIES, ARE AWARDS BADGES, PUBLISHED BEFORE WELL AS A FIRE GROSS PLANS WERE ORIGINALLY CHARACTERS IN THE STRIP TO WHICH SEEM TO IT WHEN TEMPERED IN AND HALLOWING THEY'RE SIMPLY DRAWING IN GIVES ON" PRINCIPAL SPITTLE DISTORT, READERS COMICS ARE USE, WATTERSON TOOK TWO 16-MONTHS AFTER RESISTAKES A MORE CREAT DEAL TO CALVIN OFTEN HOBBES TO ADMITS "SLIMY, "BUT IT'S NAMED A NIGHT OUT SHE IS POINT OF NOT SEEN HOBBES THE BOOKS AT THAT I REMAINING BOOK HAMSTER HUEY ARE APPEARANCE: DECEMBER 6, 1995 MOM'S FRAMES OF CALVIN GIVEN A WAGON, SOMETIMES THAT SO IT'S FATHERE'S FAMILY NO CANCELLATIONSHIP WAS PRESENTS FROM NOVEMBER 21, 1985 LAST APPEAR ABSENCE IN ANOTHERWISE IT HAPPY TO RUN IT FOR THIS DAD AS "A LITTLE TO TOLERATE CALVIN'S FAMILY DRAWN ALMOST COMMENDED UP BEING PEOPLE INSTANCE, GET MARRIED BY A DANCE CALVIN'S OUTLANDISING THE NEWSPAPER OR TABLOID NEWSPAPER BUSINESS SHOW IS ON!" AND SPRINTS OF CHILDREN'S DAD'S FRUSTRATED BY TURN HUMOR, WAS PUBLIC DIALOG THERE'S NOT MUCH AS "'94 MODERNISM" WATTERSON HAS DELIGHTS OF FANTASY LIFE WATTERSON SAYS SERVES AS AN ARTISTS IS DESTRUCTION BUSINESS, SPACEFARER OF THE OPPORTUNITIES YOU BOTH A TOPIC FOR HIS HOME TONGUE-IN-CHEEK POPULAR THAT IT WAS "HON" AND QUARTER PAGE MORE SPACIOUS CANCELLATION THE PAIR ARE CLEARLY IN PSYCHIC TRANSMOGRIFIER'S "JAP" SOUND EFFECT YOU THINKER WATTERSON ALSO GREW INCREDIBLE SPACE BUYS IN COMMONLY WHILE OTHERWISE IT'S NAME IS NOTABLE STORYLINE GAVE THE OPPORTUNITIES YOU CANCELLATION THE "CALVIN OFFER TO MAKE HIM INCORRECT ANSWERS WATTER ARTWORK OTHER OFTEN WHICH IS EVIDENT TO OTHER STRIP IS TO THEIR USE OF RULES THAT SHOWN ON SANDIFER, WHO USES A CROWQUILL BE SEEN "GLUED" TO THE ONLY PERS AND HIS FATHER SUPPORT IS LUNCHLINE GAVE THESE THIN A YEAR IN MULTIMATERIAL AND OBTAIN ON SANTASY, HIS USE, WATTERS DIALOGUE IS AN "ARTIST'S STATUS AS "A DIM VIEW IN THE ESSENTIALLY TO MAKE HIM SEEM TO INCLUDED THAT CALVIN IS AN ODD DIALOGUE MOST OF THE CLUB HAS EXPRESSION OUTSIDE AVAILABLE TO
```

It gives also the key used to decrypt the message:
```
Key to decrypt the message: AYWMCNOPHQRSTJIZKDLEGXUVFB
```

And the key used to encrypt it:
```
Key used to encrypt the message: AZERTYUIONQSDFGHJKLMWXCVBP
```

We can find the flag in the first line of the decrypted message:
```
THE FLAG IS IFONLYMODERNCRYPTOWASLIKETHIS
```

-----------------------------------------------------------------------------------

## RSA Noob - Challenge 120

Description:
```
These numbers were scratched out on a prison wall. Can you help me decode them? https://mega.nz/#!al8iDSYB!s5olEDK5zZmYdx1LZU8s4CmYqnynvU_aOUvdQojJPJQ
```

If we follow the Mega link, we'll have some sort of information and letters:

```
e: 1
c:9327565722767258308650643213344542404592011161659991421
n: 245841236512478852752909734912575581815967630033049838269083
```

That's strange, but if we google these numbers, we discover that they are used for RSA encryption (like the title says)

From wikipedia:
```
RSA (Rivest–Shamir–Adleman) is a public-key cryptosystem, one of the oldest that is widely used for secure data transmission.

In a public-key cryptosystem, the encryption key is public and distinct from the decryption key, which is kept secret private. 
An RSA user creates and publishes a public key based on two large prime numbers, along with an auxiliary value. The prime numbers are kept secret. 

Messages can be encrypted by anyone, via the public key, but can only be decoded by someone who knows the prime numbers

There are no published methods to defeat the system if a large enough key is used.


RSA is a relatively slow algorithm. Because of this, it is not commonly used to directly encrypt user data. More often, RSA is used to transmit shared keys for symmetric-key cryptography, which are then used for bulk encryption–decryption.

Decryption:
Alice can recover m from c by using her private key exponent d by computing

c^d ≡ (m^e)^d ≡ m (mod n)

Given m, she can recover the original message M by reversing the padding scheme.
```

So, we have
```
e: 1.   #Public key
c:9327565722767258308650643213344542404592011161659991421     #Cipher-text
n: 245841236512478852752909734912575581815967630033049838269083        #Module
```
If we do the reverse operation, we find that:
```
m = 9327565722767258308650643213344542404592011161659991421     #Original message (Plain-Text)
```

After that, we need to convert m from Decimal to Hexadecimal.

We can use: https://www.rapidtables.com/convert/number/decimal-to-hex.html

It converts into this Hex-text
```
61626374667B6233747465725F75705F793075725F657D
```

Finally, we can decode it
We can use this site to do the conversion from Hexadecimal to ASCII: https://www.rapidtables.com/convert/number/hex-to-ascii.html

And we are rewarded with the flag:
```
abctf{b3tter_up_y0ur_e}
```


