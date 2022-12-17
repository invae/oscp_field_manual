# domain_enumeration

Discovering Virtual hosts is the goal; always hiding from me

## non-readable dir, readble contents

Freqently associated with 403 Forbidden, directory listing may be disabled but reading/visiting contents may be allowed. 

> use known extensions such as .txt or .php (given a php website) and dir search with gobuster
```
/usr/share/wordlists/dirb/common.txt 
```


## virtual host enumeration techniques

### creative techniques
```sh
#look for deadlinks/broken images
# reload with network developer tab open
# read 404s for leaked subdomains (they are 404 b.c not yet in my etc/hosts)
```


### fuzzing

This is possible by FUZZing the Host header and measuring the responses. 


> gobuster has vhost mode; good for finding subdomains on vhosts
```sh
Example wordlist
/usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt 
```


> also possible with ffuf and similar tools, be sure to match all status codes
```sh
ffuf -u http://$ip -w /path/to/wordlist/quark-subdomains.txt -H "Host: FUZZ.target.com" -mc all
```


