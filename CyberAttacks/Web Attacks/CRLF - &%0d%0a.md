
When a browser sends a request to a web server, the web server answers back with a response containing both the HTTP response headers and the actual website content, i.e. the response body. The HTTP headers and the HTML response (the website content) are separated by a specific combination of special characters, namely a carriage return and a line feed. For short they are also known as CRLF.

The web server uses the CRLF to understand when new HTTP header begins and another one ends. The CRLF can also tell a web application or user that a new line begins in a file or in a text block. The CRLF characters are a standard HTTP/1.1 message, so it is used by any type of web server, including Apache, Microsoft IIS and all others.

## What is the CRLF Injection Vulnerability?

In a CRLF injection vulnerability attack the attacker inserts both the carriage return and linefeed characters into user input to trick the server, the web application or the user into thinking that an object is terminated and another one has started.

## CRLF injection in web applications

In web applications a CRLF injection can have severe impacts, depending on what the application does with single items. Impacts can range from information disclosure to code execution, a direct impact web application security vulnerability. In fact a CRLF injection attack can have very serious repercussions on a web application, even though it was never listed in the OWASP Top 10 list. For example it is also possible to manipulate log files in an admin panel as explained in the below example.

#### An example of CRLF Injection in a log file

Imagine a log file in an admin panel with the output stream pattern of IP - Time - Visited Path, such as the below:

```shell
123.123.123.123 - 08:15 - /index.php?page=home
```

If an attacker is able to inject the CRLF characters into the HTTP request he is able to change the output stream and fake the log entries. He can change the response from the webs application to something like the below:

```shell
/index.php?page=home&%0d%0a127.0.0.1 - 08:15 - /index.php?page=home&restrictedaction=edit
```

The %0d and %0a are the url encoded forms of CR and LF. Therefore the log entries would look like this after the attacker inserted those characters and the application displays it:

IP - Time - Visited Path

```Shell
123.123.123.123 - 08:15 - /index.php?page=home&
127.0.0.1 - 08:15 - /index.php?page=home&restrictedaction=edit
```

Therefore by exploiting a CRLF injection vulnerability the attacker can fake entries in the log file to obfuscate his own malicious actions. The attacker is literally doing page hijacking and modifying the response. For example imagine a scenario where the attacker has the admin password and executed the restrictedaction parameter, which can only be used by an admin.

The problem is that if the administrator notices that an unknown IP used the restrictedaction parameter, will notice that something is wrong. However, since now it looks like the command was issued by the localhost (and therefore probably by someone who has access to the server, like an admin) it does not look suspicious.

The whole part of the query beginning with %0d%0a will be handled by the server as one parameter. After that there is another & with the parameter restricted action which will be parsed by the server as another parameter. Effectively this would be the same query as:

```
/index.php?page=home&restrictedaction=edit
```

## HTTP Response Splitting
#### Description

Since the header of a HTTP response and its body are separated by CRLF characters an attacker can try to inject those. A combination of CRLFCRLF will tell the browser that the header ends and the body begins. That means that he is now able to write data inside the response body where the html code is stored. This can lead to a Cross-site Scripting vulnerability.

#### An example of HTTP Response Splitting leading to XSS

Imagine an application that sets a custom header, for example:

```shell
X-Your-Name: Bob
```

The value of the header is set via a get parameter called "name". If no URL encoding is in place and the value is directly reflected inside the header it might be possible for an attacker to insert the above mentioned combination of CRLFCRLF to tell the browser that the request body begins. That way he is able to insert data such as XSS payload, for example:

```shell
?name=Bob%0d%0a%0d%0a<script>alert(document.domain)</script>
```

The above will display an alert window in the context of the attacked domain.

The following simplified example uses CRLF to:

1. Add a fake HTTP response header: `Content-Length: 0`. This causes the web browser to treat this as a terminated response and begin parsing a new response.
2. Add a fake HTTP response: `HTTP/1.1 200 OK`. This begins the new response.
3. Add another fake HTTP response header: `Content-Type: text/html`. This is needed for the web browser to properly parse the content.
4. Add yet another fake HTTP response header: `Content-Length: 25`. This causes the web browser to only parse the next 25 bytes.
5. Add page content with an XSS: `<script>alert(1)</script>`. This content has exactly 25 bytes.
6. Because of the `Content-Length` header, the web browser ignores the original content that comes from the web server.

```
http://www.example.com/somepage.php?page=%0d%0aContent-Length:%200%0d%0a%0d%0aHTTP/1.1%20200%20OK%0d%0aContent-Type:%20text/html%0d%0aContent-Length:%2025%0d%0a%0d%0a%3Cscript%3Ealert(1)%3C/script%3E
```

Where %20 == 1 space

Thanks to: book.hacktricks.xyz
