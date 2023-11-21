To run these challenges, you need to install & use [Docker](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCTFs_Software%2FDocker)
## Challenge 7.1 - AjaxNotSoap  (Ajax Injection)

[For Linux System]

You need to delete the following line in the Dockerfile:
```
RUN apt-get update --fix-missing
```

#### Description :
```
Javascript is checking the login password off of an ajax call, The verification is being done on the client side.
Making a direct call to the ajax page will return the expected password

RULES = you don't have access to the 'web' folder.
```

IT: -----------------------------------------------------------------------------------------------------

Bisogna riuscire a loggarsi nel sito: 127.0.0.1:8085

Se analizziamo il JS del sito, possiamo aggiungere dei Breakpoint al suddetto
Sono presenti due grandi funzioni, una che controlla l'username e l'altra la password inserita.
Le credenziali CORRETTE sono ottenute tramite una funzione "webhooks" ajax.

Piccola digressione su cosa sono i WebHooks:
```
Nel loro nucleo, webhooks sono callback HTTP definiti dall'utente che consentono la comunicazione in tempo reale tra diverse applicazioni web. Consentono alle applicazioni di "abbonarsi" a determinati eventi e di ricevere notifiche quando questi si verificano. Di conseguenza, webhooks facilitano gli aggiornamenti automatici e asincroni tra le applicazioni, eliminando la necessità di un costante intervento manuale o di un polling ripetitivo.

Un caso d'uso comune per webhooks è quando un'applicazione vuole ricevere aggiornamenti da un altro servizio.
Ad esempio, quando un nuovo cliente si iscrive alla vostra piattaforma di e-commerce, potreste voler inviare un'e-mail di benvenuto. Invece di interrogare continuamente l'altro servizio per ottenere le informazioni sul nuovo utente, si può creare un'opzione webhook che verrà attivata quando un nuovo utente si registra. In questo modo, l'applicazione riceve i dati necessari in tempo reale, consentendo di inviare immediatamente l'e-mail di benvenuto e fornendo un'esperienza utente più reattiva.

Per approfondimenti: https://appmaster.io/it/blog/cosa-sono-i-webhook
oppure: https://it.wikipedia.org/wiki/Webhook
```

ENG: --------------------------------------------------------------------------------------------------

We need to be able to log into the site: 127.0.0.1:8085

If we analyze the JS of the site, we can add Breakpoints to the above.
There are two major functions, one that checks the username and the other the password entered.
The CORRECT credentials are obtained through an ajax "webhooks" function

Small digression on what WebHooks are::
```
At their core, webhooks are user-defined HTTP callbacks that enable real-time communication between different web applications. They allow applications to "subscribe" to certain events and receive notifications when they occur. As a result, webhooks facilitate automatic and asynchronous updates between applications, eliminating the need for constant manual intervention or repetitive polling.  
  
A common use case for webhooks is when an application wants to receive updates from another service.  
For example, when a new customer signs up for your e-commerce platform, you may want to send a welcome e-mail. Instead of continually querying the other service to get information about the new user, you can create a webhook option that will be triggered when a new user registers. This way, the application receives the necessary data in real time, allowing the welcome e-mail to be sent immediately and providing a more responsive user experience.  
  
For more information: https://appmaster.io/it/blog/cosa-sono-i-webhook  
or: https://it.wikipedia.org/wiki/Webhook  
```

#### Solution:

IT: -----------------------------------------------------------------------------------------------------

Lavorando in client-side, possiamo sfruttare il browser debugger e aggiungere breakpoints nella parte di codice in cui vengono esaminate e/o prese in comparazione i dati inseriti. Più precisamente, nel nostro caso, per l'username bisogna aggiungere un breakpoint alla riga 29 (data = data.replace(...)) {funzione Username}. Dopodiché, provando a inserire qualsiasi cosa nel campo username del sito, quest'ultimo dovrà effettuare un controllo per verificare se i dati inseriti sono corretti; ma facendolo, nella sezione SCOPES/anonymous/arguments:/data: "MrClean", apparirà in chiaro l'username cercato.

Ora, siccome abbiamo l'username, possiamo effettuare le STESSE operazioni di cui prima, fatta eccezione che nel campo username inseriamo il vero username, cioè MrClean, e nel campo password, caratteri casuali. Se abbiamo aggiunto bene il breakpoint, apparirà nella stessa sezione, la password in chiaro, o la nostra Flag = flag{hj38dsjk324nkeasd9}

Per essere sicuri, proviamo ad accedere con le credenziali appena ottenute. 

La conferma avverrà al cambio di "Username is incorrect" con la flag

ENG: --------------------------------------------------------------------------------------------------

Working in client-side, we can take advantage of the browser debugger and add breakpoints in the part of the code where the input data are examined and/or compared. More specifically, in our case, for username we need to add a breakpoint to line 29 (data = data.replace(...)) {function Username}. After that, if we try to enter anything into the username field on the site, the site will have to perform a check to see if the data entered is correct; but by doing so, in the SCOPES/anonymous/arguments:/data: "MrClean" section, the username searched for will appear in plain text.  
  
Now, since we have the username, we can do the SAME operations as before, except that in the username field we enter the real username, i.e. MrClean, and in the password field, random characters. If we have added the breakpoint right, it will appear in the same section, the plain-text password, or our Flag = flag{hj38dsjk324nkeasd9}  
  
To be sure, let's try logging in with the credentials we just obtained.   
  
Confirmation will occur when changing "Username is incorrect" with the flag  

-----------------------------------------------------------------------------------

## Challenge 7.2 - Console (Running JS function w/BrowserConsole)

[For Linux System]
#### Description :
```
You control the browser

http://127.0.0.1:8081         (use ./docker_run.sh to run the server locally)

RULES: you don't have access to web
```

Ip: 127.0.0.1:8081
#### Solution:

IT: -----------------------------------------------------------------------------------------------------

Questa volta, sul sito verremo accolti da un solo campo e da un bottone.

Possiamo inserire qualsiasi cosa per testare ma ci ritornerà sempre un NOPE.

Analizzando il JS del sito, possiamo notare che il nostro input è processato tramite funzione md5 per hasharla e se combacia con l'hash fornito nel codice, viene chiamata la funzione getThat("Y"), altrimenti getThat("N").

Come primo pensiero ho provato a decriptare l'hash fornito tramite tool online, ma nessun risultato.

Tornando a getThat(), si nota che se il contenuto di getThat() corrisponde a Y, viene chiamata una funzione ajax che andrà a recuperare il file php da "terzi". 

Come ci suggerisce il titolo della CTF, essendo getThat() una semplice funzione JS, possiamo usare la console del browser per richiamarla con qualsiasi argomento.

In questo caso, a noi serve che getThat() abbia come argomento Y, quindi chiamiamo getThat("Y").

La Flag = flag{console_control_js} è rivelata sotto il campo input.

ENG: --------------------------------------------------------------------------------------------------

This time, on the site we will be greeted by only one field and one button.  
  
We can input anything to test but it will always return a NOPE.  
  
Analyzing the JS of the site, we can see that our input is processed via md5 function to hash it and if it matches the hash provided in the code, the getThat("Y") function is called, otherwise getThat("N").  
  
As a first thought, I tried decrypting the hash provided via online tools, but no results.  
  
Returning to getThat(), we see that if the contents of getThat() match Y, an ajax function is called that will fetch the php file from "third parties."   
  
As the title of the CTF suggests, since getThat() is a simple JS function, we can use the browser console to call it with any argument.  
  
In this case, we need getThat() to have Y as an argument, so we call getThat("Y").  
  
The Flag = flag{console_control_js} is revealed below the input field.

-----------------------------------------------------------------------------------

## Challenge 7.3 - DasBlog (Privilege escalation)

[For Linux System]
#### Description :
```
RULES = you cannot access to 'web' and 'other' folders.
```

Ip: 127.0.0.1:8084

#### Solution:

IT: ---------------------------------------------------------------------------------------------------

Come prima cosa, dobbiamo effettuare il login di questo "Blog?". Andiamo alla pagina di login, e se analizziamo il codice sorgente possiamo notare un messaggio, contenente Username/Password per dei "test". Se ci logghiamo con queste credenziali e torniamo al blog principale, una volta aggiornato il sito possiamo notare 2 post, ma nessuna flag.

Analizzando il codice sorgente del sito principale, non troviamo nulla di interessante.

Non è possibile usare debugger/console perché non ci sono script da eseguire, solo pagine statiche.

Un'altra opzione è controllare i COOKIES.


Su firefox, nella sezione Storage/Cookies/http://127.0.0.1:8084, troviamo i cookie salvati in loco.

Notiamo che abbiamo dei permessi, in questo caso user. Possiamo modificare quest'ultimo in admin e auto-assegnarci ruolo di amministratore dell'intero blog. 

Se aggiorniamo la pagina, troveremo la nostra Flag = flag{C00ki3s_c4n_b33_ch4ng3d_?}

ENG: --------------------------------------------------------------------------------------------------

As the first thing, we need to login this "Blog?". We go to the login page, and if we analyze the source code we can notice a message, containing Username/Password for some "tests". If we log in with these credentials and go back to the main blog, once we refresh the site we can notice 2 posts, but no flags.

Analyzing the source code of the main site, we find nothing of interest.

It is not possible to use debugger/console because there are no scripts to run, only static pages.

Another option is to check the COOKIES.


On firefox, in the Storage/Cookies/http://127.0.0.1:8084 section, we find the cookies saved there.

We notice that we have permissions, in this case user. We can change the latter to admin and self-assign ourselves administrator role for the entire blog. 

If we refresh the page, we will find our Flag = flag{C00ki3s_c4n_b33_ch4ng3d_?}

[WEB Part_2 - Encrypted Ajax - Bruteforcing Cookies - Intro to SQLI](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FWEB_Challenges%2FWEB%20Part_2%20-%20Encrypted%20Ajax%20-%20Bruteforcing%20Cookies%20-%20Intro%20to%20SQLI)

[Deepeing into SQL Injection](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FWEB_Challenges%2FCyberAttacks%2FWeb%20Attacks%2FSQL%20Injection%20-%20'%20OR%201%3D1)
