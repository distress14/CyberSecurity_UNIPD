
### Alphabet Cipher

```Python
enigma = "OHPPHSEP: CLHUSA, VHKL, MECLP. SAL CEPUY AHY XS HUU CEO FN EOL KHO: SAL MXPHSL QXOW, WEUY PEWLP. HS AXD YLHSA, SAL CEPYD AL DMEQL YPEBL ZEROSULDD KLO ERS SE DLH.WEUY PEWLP: KN SPLHDRPL? XS'D NERPD XV NER CHOS XS. VXOY XS! X ULVS HUU SAL CEPUY AHD SALPL!OHPPHSEP: HOY DE KLO DLS DXWASD EO SAL WPHOY UXOL, XO MRPDRXS EV SALXP YPLHKD HOY VXOY SAL WPLHS SPLHDRPL ULVS FLAXOY, SAL EOL MXLZL. SAL CEPUY AHD SPRUN LOSLPLY H WPLHS MXPHSL LPH! CLHPXOW SAL DSPHC AHS DCEPO RMEO AXK FN SAL WPLHS MXPHSL, DAHOQD, KEOQLN Y. URVVN ALHYD ERS SE SAL DLH EO H GERPOLN EO SAL PEHY SE FLZEKL QXOW EV SAL MXPHSLD! DMPXST{ZEOWPHST_R_VEROY_SAL_EOL_MXLZL!}"

list={}
limit= 22
origin= ('D', 'M', 'P', 'X', 'S', 'T', 'H', 'L', 'Z', 'A', 'O', 'E', 'W', 'R', 'Y', 'V', 'U', 'C', 'N', 'K', 'Q', 'F')
sostitute=('s', 'p', 'r', 'i', 't', 'z', 'a', 'e', 'c', 'h', 'n', 'o', 'g', 'u', 'd', 'f', 'l', 'w', 'y', 'd', 'k', 'b')

for c in enigma:
	if c not in list:
		list[c] = 1
	else:
		list[c] += 1

for i in range(limit):
	og = origin[i]
	sos = sostitute[i]
	enigma = enigma.replace(og, sos)

print(enigma)
```

### Rotation Cipher:

```Python
import string

ALPHABET = list(string.printable)
LEN = len(ALPHABET)

cipher = '''%dptr*meVT%y,gWipU%y-POdnT(to*)MpfSA-&Ov-+%g-*)HVSOLof-ypg!IpvOQofidn&Ouoz$tnTyMVTSMpfyMqTSHqUZHPyyIq&Oupz(t,&OMqT)JVT!Fog!ypvOdoLOJ,+!MVU%B-&OyrTSGV$CMpUWCqUCk,*iIqTuypymepf)F-+!M+f)H,gWipU%Cofim'''

def ROTdecode(message, pos):
	rot_13dec = ''
	for c in message:
		i = ALPHABET.index(c)
		rot_13dec += ALPHABET[(i+pos)%LEN]
	return rot_13dec

dec = ROTdecode(cipher, -13)

print(dec)
```

### Ceasar cracker

```Python
def ceasar_cracker(message, from_ = -30, to_ = +30):
	for i in range(from_, to_):
		current_try = ''.join([chr(ord(c)+i) for c in message])
		print(f"Key={i}\t{current_try}")

```
