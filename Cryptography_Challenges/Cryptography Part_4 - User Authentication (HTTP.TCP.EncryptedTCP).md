## Challenge 6.1 - Sniffing (HTTP)

[For Mac/Win/Linux System]
#### Description :
```
We sniffed a sensible http traffic.
Can you identify the password?
The attacked service is called bashNinja.

Hint. Use Wireshark.
```
#### Solution :
IT: ------------------------------------------------------------------------------------------------

L'hint ci suggerisce di usare Wireshark per analizzare il traffico di rete.

Aperto il file auth.pcap con Wireshark, è possibile filtrare i pacchetti, per avere una visualizzazione più pulita e sopratutto solamente le cose che ci potrebbero interessare. 
Applichiamo quindi il filtri "http"

Ora abbiamo di fronte molte meno informazioni futili, e possiamo notare delle richieste HTPP di autenticazione, 
come "GET / HTTP/1.1."

Una di questa richiesta è:
	10464	108.812685	192.168.0.13	192.168.0.14	HTTP	377	GET / HTTP/1.1 

Una parte molto importante da analizzare è il campo "Hypertext transfer protocol".
Esaminandolo, è possible notare un campo Authorization, in cui è possibile notare la password in chiaro nel campo Credentials.

ENG: ------------------------------------------------------------------------------------------------

The hint suggests that we use Wireshark to analyze network traffic.

Opening the auth.pcap file with Wireshark, we can filter the packets, to get a cleaner view and especially only the things we might be interested in. 
We then apply the "http" filters.

Now we are looking at much less futile information, and we can see HTPP authentication requests, like "GET / HTTP/1.1."

One such request is:
	10464	108.812685	192.168.0.13	192.168.0.14	HTTP	377	GET / HTTP/1.1 

A very important part to analyze is the "Hypertext transfer protocol" field.
Examining it, you can notice an Authorization field, where you can notice the password in plain text in the Credentials field.

La flag è: "bashNinja:flag{help-me-obiwan}"

-----------------------------------------------------------------------------------

## Challenge 6.2 - gForce (Sniffing TCP)

[For Mac/Win/Linux System]
#### Description :
```
While loosing some time on the Internet you fell on a old blog-post about
conspiracy theories...

A self proclaimed hacker attached a network capture in a comment of this post
telling that he will be `0xdeadbeef` before finishing the work.

Even if the job seems risky you can't help it, you wanna look at it...
the adventure begins...
```

#### Solution :
IT: -----------------------------------------------------------------------------------------------------

Anche in questo caso ci viene fornito solamente un file exfill.pcap. Lo apriamo con Wireshark

Questa volta non abbiamo nessuna richiesta HTTP, bensì solo ARC e TCP. 
Possiamo ANALIZZARE lo stream TCP, andando in /Analyze/Follow/Stream TCP

A schermo ci dovrebbe apparire il traffico TCP, non ci interessa gran parte del testo, anche perché non è possibile "decifrarlo". A noi interessa solamente l'ultima riga di questo testo, un messaggio criptato in Base64:

ENG: ----------------------------------------------------------------------------------------------------

Again we are given only an exfill.pcap file. We open it with Wireshark

This time we do not have any HTTP requests, only ARC and TCP. 
We can ANALYZE the TCP stream by going to /Analyze/Follow/Stream TCP.

We should see the TCP traffic on the screen; we are not interested in much of the text, partly because it is not possible to "decrypt" it. We are only interested in the last line of this text, a Base64-encrypted message:

```
.SU5TQXtjMTgwN2EwYjZkNzcxMzI3NGQ3YmYzYzY0Nzc1NjJhYzQ3NTcwZTQ1MmY3N2I3ZDIwMmI4MWUxNDkxNzJkNmE3fQ==
```
IT: Se lo decriptiamo, avremmo come risultato:

ENG: If we decrypt it, we would have as a result:

```
INSA{c1807a0b6d7713274d7bf3c6477562ac47570e452f77b7d202b81e149172d6a7}
```
That is, the Flag we were looking for.

-----------------------------------------------------------------------------------

## Challenge 6.3 - Remote Multimedia Controller (TCP encrypted w/Base64)

[For Mac/Win/Linux System]
#### Description :
```
Caasi Vosima organized a party last night to show is new high-tech house to his
friends yet something went wrong with the multimedia player and the music was
turned off.

It took some time to restart the music player and the party was like frozen for a
moment. Caasi was able to recover some information collected just before the
crash.

Help Caasi to find out what happened !
```

#### Solution :

IT: -----------------------------------------
Anche in questo caso ci viene fornito un file remote-media-controler.pcap
Lo apriamo con Wireshark. Stessa situazione dell'esercizio recedente, solo richieste TCP.

Possiamo notare però un TCP diverso dagli altri, di lunghezza 4462 (4k). Se lo analizziamo, nel campo DATA troviamo un altro messaggio criptato in Base64.

ENG: --------------------------------

Again we are provided with a remote-media-controler.pcap file.
We open it with Wireshark. Same situation as in the receding exercise, just TCP requests.

However, we can notice a TCP different from the others, of length 4462 (4k). If we analyze it, in the DATA field we find another message encrypted in Base64.

```
Vmxkd1NrNVhVbk5qUlZKU1ltdGFjRlJYZEhOaWJFNVhWR3RPV0dKVmJEWldiR1JyV1ZkS1ZXRXphRnBpVkVaVFYycEtVMU5IUmtobFJYQlRUVmhDTmxZeFdtdGhhelZ5WWtWYWFWSlViRmRVVlZaYVRURmFjbFpyT1ZaV2JXUTJWa1pvYTFkck1YVlVhbHBoVWxack1GUlZaRXRqVmxaMVZHMTRXRkpVUlRCWFdIQkdUbGRHY2s1VmFFOVdNWEJoV1Zkek1XSldaSFJPVm1SclZsZDRXbFJWVm5wUVVUMDk=
```
Let's decrypt it:

```
VldwSk5XUnNjRVJSYmtacFRXdHNibE5XVGtOWGJVbDZWbGRrWVdKVWEzaFpiVEZTV2pKU1NHRkhlRXBTTVhCNlYxWmthazVyYkVaaVJUbFdUVVZaTTFaclZrOVZWbWQ2VkZoa1drMXVUalphUlZrMFRVZEtjVlZ1VG14WFJURTBXWHBGTldGck5VaE9WMXBhWVdzMWJWZHROVmRrVld4WlRVVnpQUT09
```
IT: Sembra che non sia cambiato nulla, ma il risultato della conversione è un altro messaggio criptato in Base64. Di conseguenza lo possiamo nuovamente decriptare:

ENG: Nothing seems to have changed, but the result of the conversion is another Base64-encrypted message. As a result we can decrypt it again:

```
VWpJNWRscERRbkZpTWtsblNWTkNXbUl6VldkYWJUa3hZbTFSWjJSSGFHeEpSMXB6V1Zkak5rbEZiRTlWTUVZM1ZrVk9VVmd6VFhkWk1uTjZaRVk0TUdKcVVuTmxXRTE0WXpFNWFrNUhOV1paYWs1bVdtNVdkVWxZTUVzPQ==
```
Again:

```
UjI5dlpDQnFiMklnSVNCWmIzVWdabTkxYm1RZ2RHaGxJR1pzWVdjNklFbE9VMEY3VkVOUVgzTXdZMnN6ZEY4MGJqUnNlWE14YzE5ak5HNWZZak5mWm5WdUlYMEs=
```
Again:

```
R29vZCBqb2IgISBZb3UgZm91bmQgdGhlIGZsYWc6IElOU0F7VENQX3MwY2szdF80bjRseXMxc19jNG5fYjNfZnVuIX0K
```
And again:

```
Good job ! You found the flag: INSA{TCP_s0ck3t_4n4lys1s_c4n_b3_fun!}
```


Next => [WEB Part_1 - Ajax - Console - Cookies(Privilege escalation)](<obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FWEB_Challenges%2FWEB%20Part_1%20-%20Ajax%20-%20Console%20-%20Cookies(Privilege%20escalation)>)

[If you want to keep practicing - PicoCTF](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FEasy%20CTFs%2FStarting%20with%20Cryptography%20CTFs%20-%20PicoCTF.org)

[If you want to keep practicing - CTFLearn](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FEasy%20CTFs%2FStarting%20with%20Cryptography%20CTFs%20-%20CTFlearn.com)

Previous => [Cryptography Part_3 - Hash Cracking - XOR - Algorithm Cryptoanalysis](obsidian://open?vault=Default&file=GitHub%20Uploads%2FCyberSecurity_UNIPD%2FCryptography_Challenges%2FCryptography%20Part_3%20-%20Hash%20Cracking%20-%20XOR%20-%20Algorithm%20Cryptoanalysis)

