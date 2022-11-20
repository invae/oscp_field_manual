# web domain enumeration

Discovering Virtual hosts is the goal; always hiding from me


## non-readable dir, readble contents
freqently associated with 403 Forbidden

> use known extensions such as .txt or .php (given a php website) and dir seach with gobuster
```
/usr/share/wordlists/dirb/common.txt 
```


## subdomain enumeration

> creative subdomain enumeration
```sh
#look for deadlinks/broken images
# reload with network developer tab open
# read 404s for leaked subdomains (they are 404 b.c not yet in my etc/hosts)
```

> gobuster has vhost mode; good for finding subdomains on vhosts (huge weakpoint for me rn)
```sh
Example wordlist
/usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt 
```

> also possible with wfuzz with a lengthy syntax
```sh
TODO
```


