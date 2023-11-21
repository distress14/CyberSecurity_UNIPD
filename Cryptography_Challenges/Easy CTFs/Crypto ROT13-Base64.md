
Description:
```
This time you intercepted a communication between Professor Conti and his
teaching assistants. But this is encrypted!

Luckily, we know that their common encryption mechanisms is:

1. from plain message to Base64
2. Transform the Base64 with a Rotation Cipher of 13 positions

In order to read it, you need to perform the encrypting operation in reverse.

Good luck!
```

encrypted_flag.txt:
```
%dptr*meVT%y,gWipU%y-POdnT(to*)MpfSA-&Ov-+%g-*)HVSOLof-ypg!IpvOQofidn&Ouoz$tnTyMVTSMpfyMqTSHqUZHPyyIq&Oupz(t,&OMqT)JVT!Fog!ypvOdoLOJ,+!MVU%B-&OyrTSGV$CMpUWCqUCk,*iIqTuypymepf)F-+!M+f)H,gWipU%Cofim
```

Pretty forward, we can try to: 

Chiper-text -> ROTdecode(chiper, -13) -> Base64Decode -> Plain-Text

So:
```Python
import base64
import string

ALPHABET = list(string.printable)
LEN = len(ALPHABET)

def ROTdecode(message, pos):
	rot_13dec = ''
	for c in message:
		i = ALPHABET.index(c)
		rot_13dec += ALPHABET[(i+pos)%LEN]
	return rot_13dec

def base64Decode(message):
	b64_dec = message.encode('ascii')
	b64_dec = base64.b64decode(b64_dec)
	b64_dec = b64_dec.decode('ascii')
	return b64_dec

cipher = '''%dptr*meVT%y,gWipU%y-POdnT(to*)MpfSA-&Ov-+%g-*)HVSOLof-ypg!IpvOQofidn&Ouoz$tnTyMVTSMpfyMqTSHqUZHPyyIq&Oupz(t,&OMqT)JVT!Fog!ypvOdoLOJ,+!MVU%B-&OyrTSGV$CMpUWCqUCk,*iIqTuypymepf)F-+!M+f)H,gWipU%Cofim'''

dec = ROTdecode(cipher, -13)
dec = base64Decode(dec)

print(dec)
```

The output (with the Flag) will be:
```
GG you decrypted the message between Professor Conti and his assistants.
You are a step closer to pass the exam!
spritz{another_useless_encryption}
```

