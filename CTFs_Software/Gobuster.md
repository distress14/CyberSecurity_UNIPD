[23.10.2023]
Website Bruteforce

Gobuster is used to extract information about the target. Gobuster is written in GO-Lang. Some very common scanners like [**dirbuster**](https://www.securitynewspaper.com/2018/11/14/find-hidden-directories-on-web-server/)or other scanners.

Works w/MAC Air M1
## GOBUSTER INSTALLATION

Install Homebrew
Follow on: https://brew.sh

Open the terminal, install Gobuster brew

```terminal
brew install gobuster
```

After installation, type gobuster
```
User@User-Air-2 ~ % gobuster
Usage:
  gobuster [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
  gcs         Uses gcs bucket enumeration mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  tftp        Uses TFTP enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)

Flags:
      --debug                 Enable debug output
      --delay duration        Time each thread waits between requests (e.g. 1500ms)
  -h, --help                  help for gobuster
      --no-color              Disable color output
      --no-error              Don't display errors
  -z, --no-progress           Don't display progress
  -o, --output string         Output file to write results to (defaults to stdout)
  -p, --pattern string        File containing replacement patterns
  -q, --quiet                 Don't print the banner and other noise
  -t, --threads int           Number of concurrent threads (default 10)
  -v, --verbose               Verbose output (errors)
  -w, --wordlist string       Path to the wordlist. Set to - to use STDIN.
      --wordlist-offset int   Resume from a given position in the wordlist (defaults to 0)
```

## FINDING FILES/ DIRECTORIES

- On Target side we will be using **DVWA (Dam Vulnerable Web Application)**. Download from [https://www.vulnhub.com/entry/damn-vulnerable-web-application-dvwa-107,43/]
- Type **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt**
- **-u** is used to assign target URL, **192.168.1.105** is our target/DVWA.
- **-w** is used to assign wordlist.  **/usr/share/wordlists/dirb/common.txt** is the wordlist location.

```
root@kali:/home/iicybersecurity# **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Timeout:        10s
 2019/11/01 01:20:19 Starting gobuster
 /.hta (Status: 403)
 /.svn (Status: 301)
 /.htpasswd (Status: 403)
 /.svn/entries (Status: 200)
 /.htaccess (Status: 403)
 /css (Status: 301)
 /images (Status: 301)
 /includes (Status: 301)
 /js (Status: 301)
 2019/11/01 01:20:25 Finished

```
- Above query has scanned all the files & directories on the target URL.


## PRINTING FILES WITH FULL PATH

- Type **gobuster dir -e -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt**
- **-e** is used to print full path of the files.
- **-u** is used to assign target URL **192.168.1.105** is our target.
- **-w** is used to assign wordlist.  **/usr/share/wordlists/dirb/common.txt** is the wordlist location.

```
root@kali:/home/iicybersecurity# **gobuster dir -e -u  http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Expanded:       true
 [+] Timeout:        10s
 2019/11/01 01:21:34 Starting gobuster
 http://192.168.1.105/dvwa/.hta (Status: 403)
 http://192.168.1.105/dvwa/.htpasswd (Status: 403)
 http://192.168.1.105/dvwa/.svn (Status: 301)
 http://192.168.1.105/dvwa/.htaccess (Status: 403)
 http://192.168.1.105/dvwa/.svn/entries (Status: 200)
 http://192.168.1.105/dvwa/css (Status: 301)
 http://192.168.1.105/dvwa/images (Status: 301)
 http://192.168.1.105/dvwa/includes (Status: 301)
 http://192.168.1.105/dvwa/js (Status: 301)
 2019/11/01 01:21:39 Finished

```
- Above you can find the full path of the target URL. This query can help to prepare for the initial level of information gathering.


## PRINTING OUTPUT USING VERBOSE

- Type **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -v**
- **-u** is used to assign target URL. **192.168.1.105** is our target.
- **-w** is used to assign wordlist.  **/usr/share/wordlists/dirb/common.txt** is the wordlist location.
- **-v** is used for verbose mode.
```
root@kali:/home/iicybersecurity# **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -v**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Verbose:        true
 [+] Timeout:        10s
 2019/11/01 01:33:32 Starting gobuster
 Missed: /.bashrc (Status: 404)
 Missed: /.cvs (Status: 404)
 Missed: /.cvsignore (Status: 404)
 Missed: /.forward (Status: 404)
 Missed: /.config (Status: 404)
 Missed: /.git/HEAD (Status: 404)
 Missed: /.cache (Status: 404)
 Found: /.hta (Status: 403)
 Missed: /.profile (Status: 404)
 Missed: /.history (Status: 404)
 Missed: /.mysql_history (Status: 404)
 Missed: /.passwd (Status: 404)
 Missed: /.listings (Status: 404)
 Missed: /.perf (Status: 404)
 Missed: /.sh_history (Status: 404)
 Found: /.htpasswd (Status: 403)
 Missed: /.listing (Status: 404)
 Missed: /.rhosts (Status: 404)
 Found: /.svn/entries (Status: 200)
 Missed: /.subversion (Status: 404)
 Missed: /.ssh (Status: 404)
 Missed: /.web (Status: 404)
 Missed: /_archive (Status: 404) Found: /.svn (Status: 301) Missed: /@ (Status: 404) Missed: /.swf (Status: 404) Found: /.htaccess (Status: 403) Missed: /_backup (Status: 404) Missed: /.bash_history (Status: 404) Missed: /_adm (Status: 404) Missed: /_borders (Status: 404) Missed: /_cache (Status: 404) Missed: /_admin (Status: 404) Missed: /_baks (Status: 404) Missed: /_catalogs (Status: 404) Missed: /_code (Status: 404) Missed: /_assets (Status: 404) Missed: /_common (Status: 404) Missed: /_conf (Status: 404) Missed: /_ajax (Status: 404) Missed: /_ (Status: 404)
 Missed: /_files (Status: 404)
 Missed: /_css (Status: 404)
 Missed: /_data (Status: 404)
 Missed: /_database (Status: 404)
 Missed: /_db_backups (Status: 404)
 Missed: /_derived (Status: 404)
 Missed: /_dev (Status: 404)
 Missed: /_config (Status: 404)
 Missed: /_flash (Status: 404)
 Missed: /_dummy (Status: 404)
 Missed: /_inc (Status: 404)
 Missed: /_fpclass (Status: 404)
 Missed: /_includes (Status: 404)
 Missed: /_install (Status: 404)
 Missed: /_images (Status: 404)
 Missed: /_js (Status: 404)
 Missed: /_layouts (Status: 404)
 Missed: /_img (Status: 404)
 Missed: /_lib (Status: 404)
 Missed: /_media (Status: 404)
 Missed: /_mm (Status: 404)
 Missed: /_mygallery (Status: 404)
```
- Above query has try to find files in verbose mode. Showing HTTP status code on each request.

## PRINTING FILES WITH NO STATUS 

- Type **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -n**
- **-u** is used to assign target URL. **192.168.1.105** is our target URL.
- **-w** is used to assign wordlist.  **/usr/share/wordlists/dirb/common.txt** is the wordlist location.
- **-n** is used to print with **no status codes**.

```
root@kali:/home/iicybersecurity# **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -n**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] No status:      true
 [+] Timeout:        10s
 2019/11/01 02:36:35 Starting gobuster
 /.hta
 /.htpasswd
 /.svn
 /.svn/entries
 /.htaccess
 /css
 /images
 /includes
 /js
 2019/11/01 02:36:38 Finished
```
- Above query has printed with data without any status codes.


## FINDING LENGTH OF THE RESPONSE FILES

- Type **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -l**
- -u is used to assign target URL. 192.168.1.105 is our target URL.
- -w is used to assign wordlist location.  **-w /usr/share/wordlists/dirb/common.txt** is our wordlist location.
- -l is used find length of response files.

```
root@kali:/home/iicybersecurity# **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -l**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Show length:    true
 [+] Timeout:        10s
 2019/11/01 02:57:45 Starting gobuster
 /.hta (Status: 403) [Size: 1108]
 /.htpasswd (Status: 403) [Size: 1108]
 /.svn/entries (Status: 200) [Size: 256]
 /.htaccess (Status: 403) [Size: 1108]
 /.svn (Status: 301) [Size: 416]
 /css (Status: 301) [Size: 415]
 /images (Status: 301) [Size: 418]
 /includes (Status: 301) [Size: 420]
 /js (Status: 301) [Size: 414]
 2019/11/01 02:57:48 Finished
```
- Above shows the files size. By this attacker can obtain type of files target uses to maintain their website and as per **[digital forensics](https://www.iicybersecurity.com/digital-forensic.html)** expert of International Institute of Cyber Security file size is also one of the parameters in analyzing the malware.

## FINDING FILES WITH SPECIFIC EXTENSION

- Type **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -x .php**
- **-u** is used to assign URL. 192.168.1.105 is our target URL
- **-w** is used to assign wordlist. **-w /usr/share/wordlists/dirb/common.txt** is wordlist location.
- **-x** is used to extract specific extension files. **.php** will be extracted.

```
root@kali:/home/iicybersecurity# **gobuster dir -u http://192.168.1.105/dvwa -w /usr/share/wordlists/dirb/common.txt -x .php**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://192.168.1.105/dvwa
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Extensions:     php
 [+] Timeout:        10s
 2019/11/01 03:32:20 Starting gobuster
 /.hta (Status: 403)
 /.hta.php (Status: 403)
 /.htpasswd (Status: 403)
 /.htpasswd.php (Status: 403)
 /.htaccess (Status: 403)
 /.htaccess.php (Status: 403)
 /.svn/entries (Status: 200)
 /.svn (Status: 301)
 /css (Status: 301)
 /images (Status: 301)
 /includes (Status: 301)
 /js (Status: 301)
 2019/11/01 03:32:25 Finished
```
- Above query has found files with .php extension. This query can help attacker to create malicious files on specific extension.


## FINDING USERNAME & PASSWORD

- Type **gobuster dir -u http://testphp.vulnweb.com/login.php -w /usr/share/wordlists/dirb/common.txt -U test -P test**
- **-u** is used to assign URL. 192.168.1.105 is our target URL
- **-w** is used to assign wordlist. **-w /usr/share/wordlists/dirb/common.txt** is wordlist location.
- **-U** is for username & **-P** is for password.

```
root@kali:/home/iicybersecurity# **gobuster dir  -u http://testphp.vulnweb.com/login.php -w /usr/share/wordlists/dirb/common.txt -U test -P test**
 Gobuster v3.0.1
 by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
 [+] Url:            http://testphp.vulnweb.com/login.php
 [+] Threads:        10
 [+] Wordlist:       /usr/share/wordlists/dirb/common.txt
 [+] Status codes:   200,204,301,302,307,401,403
 [+] User Agent:     gobuster/3.0.1
 [+] Auth User:      test
 [+] Timeout:        10s
 2019/11/01 04:31:34 Starting gobuster
 /admin.php (Status: 200)
 /index.php (Status: 200)
 /info.php (Status: 200)
 /phpinfo.php (Status: 200)
 /xmlrpc.php (Status: 200)
 /xmlrpc_server.php (Status: 200)
 2019/11/01 04:32:54 Finished
```
- Above query has returned with address of 200 which means that username & password has matched.


Video Step by Step: https://youtu.be/PSwIv1V9Y10

