# tips and notes on php websites

> for testing proof of concept; debugging logic; understanding some script or shel
```
php -a 			; enter php interactive mode, test the effects of syntax etc, etc
```

> index.php
```
if it exists, the webiste is running php
```


# common php website vulnerabilities

## local file inclusion - LFI

> defintion
```
when a website pulls a picture saved on the machine to display it
when a website pulls another file and displays it
the website is misconfigured and is allowed to serve any file on the server
```

> useful tactics
```
php://filter/convert.base64-encode/resource=PATH_TO_FILE 		

wordlist for discovering readables through LFI
/usr/share/wordlists/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt
deliver the wordlist with wfuzz or another tool

/proc/self/cwd/KNOWN_FILE	; for dealing with unknown path, but known dir contents

```


