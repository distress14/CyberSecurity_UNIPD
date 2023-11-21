
Crack the code in this beginner-friendly challenge series.

## substitution0
### Description
```
A message has come in but it seems to be all scrambled. 
Luckily it seems to have the key at the beginning. 
Can you crack this substitution cipher?

Download the message https://artifacts.picoctf.net/c/152/message.txt.
```

Here's the downloaded/encrypted file:
```
DECKFMYIQJRWTZPXGNABUSOLVH 

Ifnfuxpz Wfyndzk dnpaf, oqbi d yndsf dzk abdbfwv dqn, dzk enpuyib tf bif effbwf
mnpt d ywdaa cdaf qz oiqci qb oda fzcwpafk. Qb oda d efdubqmuw acdndedfua, dzk, db
bidb bqtf, uzrzpoz bp zdbundwqaba—pm cpunaf d ynfdb xnqhf qz d acqfzbqmqc xpqzb
pm sqfo. Bifnf ofnf bop npuzk ewdcr axpba zfdn pzf flbnftqbv pm bif edcr, dzk d
wpzy pzf zfdn bif pbifn. Bif acdwfa ofnf flcffkqzywv idnk dzk ywpaav, oqbi dww bif
dxxfdndzcf pm eunzqaifk ypwk. Bif ofqyib pm bif qzafcb oda sfnv nftdnrdewf, dzk,
bdrqzy dww biqzya qzbp cpzaqkfndbqpz, Q cpuwk idnkwv ewdtf Juxqbfn mpn iqa pxqzqpz
nfaxfcbqzy qb.

Bif mwdy qa: xqcpCBM{5UE5717U710Z_3S0WU710Z_59533D2F}
```

It seams that we need a substitution cipher to solve it.

We can check the letters frequency using python
```python
letter_frequency = {}

for c in cipher:
	if c not in letter_frequency:
		letter_frequency[c] = 1
	else:
		letter_frequency[c] += 1

sorted_frequency = sorted(letter_frequency.items(), key=lambda kv: kv[1], reverse = True)

print(sorted_frequency)
```

```
[(' ', 98), ('f', 59), ('d', 49), ('b', 38), ('z', 35), ('q', 34), ('n', 31), ('p', 31), ('a', 28), ('i', 22), ('w', 21), ('c', 17), ('k', 16), ('y', 14), ('u', 12), ('o', 12), ('\n', 11), ('x', 10), (',', 10), ('m', 10), ('e', 9), ('B', 6), ('v', 6), ('t', 6), ('.', 5), ('r', 5), ('U', 4), ('5', 4), ('7', 4), ('Q', 3), ('W', 3), ('Z', 3), ('s', 3), ('1', 3), ('0', 3), ('3', 3), ('D', 2), ('E', 2), ('C', 2), ('F', 2), ('M', 2), ('I', 2), ('J', 2), ('S', 2), ('l', 2), ('_', 2), ('K', 1), ('Y', 1), ('R', 1), ('T', 1), ('P', 1), ('X', 1), ('G', 1), ('N', 1), ('A', 1), ('O', 1), ('L', 1), ('V', 1), ('H', 1), ('—', 1), ('h', 1), (':', 1), ('{', 1), ('9', 1), ('2', 1), ('}', 1)]
```

We need first to know (100% sure) if our substitution is done, so to find that, we can uppercase all the cipher and substitute with lower letters:
```python
cipher = cipher.upper()
```

We can create 2 tuple (respectively og: original & sub: substitute) to pick from when it's time for replacing. We put a limit to control it better.

I'll first start translating the "back" of the flag:
```python
limit = 7

og_tuple = ('X','Q','C','P','B','M','','','','','','','','','','')
sub_tuple = ('p','i','c','o','t','f','','','','','','','','','','')

for i in range(limit):
	og = og_tuple[i]
	sub = sub_tuple[i]
	cipher = cipher.replace(og,sub)

print(cipher)
```

If we continue to add letters:
```python
limit = 22

og_tuple = ('X','Q','C','P','B','M','Z','A','F','D','K','N','Y','I','W','U','V','R','E','T','O','S')
sub_tuple = ('p','i','c','o','t','f','n','s','e','a','d','r','g','h','l','u','y','k','b','m','w','v')

for i in range(limit):
	og = og_tuple[i]
	sub = sub_tuple[i]
	cipher = cipher.replace(og,sub)
```

We'll complete the cipher & we'll find the flag:
```
hereupon legrand arose, with a grave and stately air, and brought me the beetle
from a glass case in which it was enclosed. it was a beautiful scarabaeus, and, at
that time, unknown to naturalists—of course a great priHe in a scientific point
of view. there were two round black spots near one eLtremity of the back, and a
long one near the other. the scales were eLceedingly hard and glossy, with all the
appearance of burnished gold. the weight of the insect was very remarkable, and,
taking all things into consideration, i could hardly blame Jupiter for his opinion
respecting it.

the flag is: picoctf{5ub5717u710n_3v0lu710n_59533a2e}
```


-----------------------------------------------------------------------------------

## substitution1
### Description
```
A second message has come in the mail, and it seems almost identical to the first one. 
Maybe the same thing will work again.
Download the message https://artifacts.picoctf.net/c/183/message.txt.
```

Here's the downloaded/encrypted file:
```
LKOb (bwvek ove lgqkhej kwj osgx) gej g kyqj vo lvrqhkje bjlhetky lvrqjktktvu. Lvukjbkgukb gej qejbjukjz dtkw g bjk vo lwgssjuxjb dwtlw kjbk kwjte lejgktftky, kjlwutlgs (guz xvvxstux) bitssb, guz qevmsjr-bvsftux gmtstky. Lwgssjuxjb hbhgssy lvfje g uhrmje vo lgkjxvetjb, guz dwju bvsfjz, jglw ytjszb g bketux (lgssjz g osgx) dwtlw tb bhmrtkkjz kv gu vustuj blvetux bjeftlj. LKOb gej g xejgk dgy kv sjgeu g dtzj geegy vo lvrqhkje bjlhetky bitssb tu g bgoj, sjxgs juftevurjuk, guz gej wvbkjz guz qsgyjz my rguy bjlhetky xevhqb gevhuz kwj dvesz ove ohu guz qeglktlj. Ove kwtb qevmsjr, kwj osgx tb: qtlvLKO{OE3AH3ULY_4774LI5_4E3_L001_6J0659OM}
```

We procede like with substitution0:
```python
limit = 23

og_tuple = ('Q','T','L','V','K','O','W','J','B','G','E','S','X','Y','U','Z','R','H','M','F','I','D','A','','','','')
sub_tuple = ('p','i','c','o','t','f','h','e','s','a','r','l','g','y','n','d','m','u','b','v','k','w','q','','','','')

cipher = cipher.upper()

for i in range(limit):
	og = og_tuple[i]
	sub = sub_tuple[i]
	cipher = cipher.replace(og,sub)

print(cipher)
```

We'll complete the cipher & we'll find the flag:
```
 ctfs (short for capture the flag) are a type of computer security competition. 
contestants are presented with a set of challenges which test their creativity, 
technical (and googling) skills, and problem-solving ability. challenges usually cover a number of categories, and when solved, each yields a string (called a flag) which is submitted to an online scoring service. 
ctfs are a great way to learn a wide array of computer security skills in a safe, legal environment, and are hosted and played by many security groups around the world for fun and practice. 
for this problem, the flag is: picoctf{fr3qu3ncy_4774ck5_4r3_c001_6e0659fb}
```


-----------------------------------------------------------------------------------

## substitution2 - OPEN
### Description
```
It seems that another encrypted message has been intercepted. 
The encryptor seems to have learned their lesson though and now there isn't any punctuation! 
Can you still crack the cipher?
Download the message https://artifacts.picoctf.net/c/114/message.txt.
```

Here's the downloaded/encrypted file:
```
fnjdjjzqsfsjpjdxwmfnjdcjwwjsfxhwqsnjynqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgsqgkwayqgekthjdvxfdqmfxgyaskthjdknxwwjgejfnjsjkmuvjfqfqmgslmkasvdquxdqwtmgstsfjusxyuqgqsfdxfqmglagyxujgfxwscnqknxdjpjdtasjlawxgyuxdojfxhwjsoqwwsnmcjpjdcjhjwqjpjfnjvdmvjdvadvmsjmlxnqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgqsgmfmgwtfmfjxknpxwaxhwjsoqwwshafxwsmfmejfsfayjgfsqgfjdjsfjyqgxgyjzkqfjyxhmafkmuvafjdskqjgkjyjljgsqpjkmuvjfqfqmgsxdjmlfjgwxhmdqmasxllxqdsxgykmujymcgfmdaggqgeknjkowqsfsxgyjzjkafqgekmglqeskdqvfsmlljgsjmgfnjmfnjdnxgyqsnjxpqwtlmkasjymgjzvwmdxfqmgxgyquvdmpqsxfqmgxgymlfjgnxsjwjujgfsmlvwxtcjhjwqjpjxkmuvjfqfqmgfmaknqgemgfnjmlljgsqpjjwjujgfsmlkmuvafjdsjkadqftqsfnjdjlmdjxhjffjdpjnqkwjlmdfjknjpxgejwqsufmsfayjgfsqgxujdqkxgnqensknmmwsladfnjdcjhjwqjpjfnxfxgagyjdsfxgyqgemlmlljgsqpjfjkngqiajsqsjssjgfqxwlmdumagfqgexgjlljkfqpjyjljgsjxgyfnxffnjfmmwsxgykmglqeadxfqmglmkasjgkmagfjdjyqgyjljgsqpjkmuvjfqfqmgsymjsgmfwjxysfayjgfsfmogmcfnjqdjgjutxsjlljkfqpjwtxsfjxknqgefnjufmxkfqpjwtfnqgowqojxgxffxkojdvqkmkflqsxgmlljgsqpjwtmdqjgfjynqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgfnxfsjjosfmejgjdxfjqgfjdjsfqgkmuvafjdskqjgkjxumgenqensknmmwjdsfjxknqgefnjujgmaenxhmafkmuvafjdsjkadqftfmvqiajfnjqdkadqmsqftumfqpxfqgefnjufmjzvwmdjmgfnjqdmcgxgyjgxhwqgefnjufmhjffjdyjljgyfnjqduxknqgjsfnjlwxeqsvqkmKFL{G6D4U_4G41T515_15_73Y10A5_42JX1770}
```

We can procede like with substitution0 & substitution1, but we need to be more carefully cause there's no space between words
```python
frequency_counter = {}

for c in cipher:
	if c not in frequency_counter:
		frequency_counter[c] = 1
	else:
		frequency_counter[c] += 1

sorted_frequency = sorted(frequency_counter.items(), key=lambda kv: kv[1], reverse = True)
#print(frequency_counter)

cipher = cipher.upper()

limit = 18

og_tuple =('V','Q','K','M','F','L','J','F','Q','G','','X','K','D','N','W','A','','','','','','','','','','')
sub_tuple =('p','i','c','o','t','f','e','t','a','n','','s','r','h','d','l','u','','','','','','','','','','')

for i in range(limit):
	og = og_tuple[i]
	sub = sub_tuple[i]
	cipher = cipher.replace(og,sub)

print(cipher)

```

This CTF is not Finished. TODO
```
tdeheeZiStSePehslotdehCelleStsHliSdeYdiEdScdoolcoUputehSecuhitTcoUpetitionSincluYinEcTHehpsthiotsnYuScTHe
hcdsllenEetdeSecoUpetitionSfocuSphiUshilTonSTSteUSsYUiniSthstionfunYsUentslSCdicdshePehTuSefulsnYUshOetsHleSOillSdoCe
PehCeHeliePetdephopehpuhpoSeofsdiEdScdoolcoUputehSecuhitTcoUpetitioniSnotonlTtotescdPslusHleSOillSHutslSotoEetStuYent
SinteheSteYinsnYeZciteYsHoutcoUputehScienceYefenSiPecoUpetitionSsheoftenlsHohiouSsffsihSsnYcoUeYoCntohunninEcdecOliSt
SsnYeZecutinEconfiESchiptSoffenSeontdeotdehdsnYiSdesPilTfocuSeYoneZplohstionsnYiUphoPiSstionsnYoftendsSeleUentSofplsT
CeHeliePescoUpetitiontoucdinEontdeoffenSiPeeleUentSofcoUputehSecuhitTiStdehefohesHettehPediclefohtecdePsnEeliSUtoStuY
entSinsUehicsndiEdScdoolSfuhtdehCeHeliePetdstsnunYehStsnYinEofoffenSiPetecdniIueSiSeSSentislfohUountinEsneffectiPeYef
enSesnYtdsttdetoolSsnYconfiEuhstionfocuSencounteheYinYefenSiPecoUpetitionSYoeSnotlesYStuYentStoOnoCtdeiheneUTsSeffect
iPelTsStescdinEtdeUtosctiPelTtdinOliOesnsttscOehpicoctfiSsnoffenSiPelTohienteYdiEdScdoolcoUputehSecuhitTcoUpetitiontd
stSeeOStoEenehsteinteheStincoUputehSciencesUonEdiEdScdoolehStescdinEtdeUenouEdsHoutcoUputehSecuhitTtopiIuetdeihcuhioS
itTUotiPstinEtdeUtoeZploheontdeihoCnsnYensHlinEtdeUtoHettehYefenYtdeihUscdineStdeflsEiS
picoctf{n6h4U_4n41T515_15_73Y10u5_42es1770}
```

-----------------------------------------------------------------------------------