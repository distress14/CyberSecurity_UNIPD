
WEB: https://ctflearn.com/challenge/1116.   [23.10.2023]
## What's given

Some ghosts made this site ?, it's a little spooky but theres a bunch of stuff hidden around.
https://gobustme.ctflearn.com/

## What I have done

# Beware haunted website! 👻

Ghosts invaded my home and my website. They are driving me crazy. They turn on the TV and are watching Ghostbusters films and animes all day long. and hide somewhere the flag

Arg! I hear again the opening on the TV... help me!

Ghostbusters Opening Song: https://www.youtube.com/watch?v=W-485a-qj4I

Ghostbusters [Gobuster!](https://www.securitynewspaper.com/2019/11/04/bruteforce-any-website-with-gobuster-step-by-step-guide/)
If there's something strange
In your neighborhood
Who you gonna call?
Ghostbusters Gobuster!
If there's something weird
And it don't look good
Who you gonna call?
Ghostbusters Gobuster!
I ain't 'fraid of no ghost
I ain't 'fraid of no ghost
If you're seeing things
Running through your head
Who can you call?
Ghostbusters Gobuster!
An invisible man
Sleepin' in your bed
Ow, who you gonna call?
Ghostbusters Gobuster!
I ain't 'fraid of no ghost
I ain't 'fraid of no ghost
Who you gonna call?
Ghostbusters Gobuster!
If you're all alone
Pick up the phone
And call
Ghostbusters Gobuster!
I ain't 'fraid of no ghost
Ooh, I hear it likes the girls
Hm, I ain't 'fraid of no ghost
Yeah, yeah, yeah, yeah
Who you gonna call?
Ghostbusters Gobuster!
Mmm, if you've had a dose of a
Freaky ghost, baby
You better call
Ghostbusters Gobuster!
Ow!
Lemme tell yaâ€¦ 
A [common wordlist](https://raw.githubusercontent.com/v0re/dirb/master/wordlists/common.txt) may help you too!

## Gobuster Guide

You need to have Homebrew installed to download Gobuster.
Follow on: https://brew.sh

Open the terminal, and install Gobuster with Homebrew

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

## Starting with something?

Type
```
gobuster dir -u https://gobustme.ctflearn.com -w /Users/andrea/CTF/Gobustme?/Gobustme_Wordlist.txt
```

- **-u** is used to assign target URL, [https://gobustme.ctflearn.com] is our target
- **-w** is used to assign wordlist. /Users/andrea/CTF/Gobustme?/Gobustme_Wordlist.txt is the wordlist location.

Result
```
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://gobustme.ctflearn.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /Users/andrea/CTF/Gobustme ?/Gobustme_Wordlist.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/call                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/call/]
/carpet               (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/carpet/]
/flag                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/flag/]
/hide                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/hide/]
/index.html           (Status: 200) [Size: 2713]
/sex                  (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/sex/]
/shadow               (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/shadow/]
/skin                 (Status: 301) [Size: 169] [--> http://gobustme.ctflearn.com/skin/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================
```


## Link checking

http://gobustme.ctflearn.com/call/
```
<html>
	<head></head>
	<body>Who you gonna call? Ghostbusters! 👻</body>
</html>
```
Nothing interesting


http://gobustme.ctflearn.com/carpet/
```
<html>
	<head></head>
	<body>My sheet is dirty, do you mind if I use your carpet instead? 👻</body>
</html>
```
Nothing interesting


http://gobustme.ctflearn.com/flag/
```
<html>
	<head></head>
	<body>No, too easy :)</body>
</html>
```
I could have expected this


http://gobustme.ctflearn.com/hide/
```
<html>
	<head></head>
	<body>It was well hidden isn't it? CTFlearn{gh0sbu5t3rs_4ever} 👻</body>
</html>
```
Flag found: CTFlearn{gh0sbu5t3rs_4ever}


Wordlist Used (Given by the CTF author):
https://raw.githubusercontent.com/v0re/dirb/master/wordlists/common.txt

