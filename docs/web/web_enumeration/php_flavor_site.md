
# php_flavor_site

## tips and notes on php websites

> for testing proof of concept; debugging logic; understanding some script or shell code
```
php -a 			; enter php interactive mode, test the effects of syntax etc, etc
```


> index.php
```
if it exists, the webiste is running php
```


> if having trouble finding the `config.php` type files in post exploitation, search for these near top of the file
```php
require_once( path/to/config.php );
```


## common php website vulnerabilities

### local file inclusion - LFI

> defintion
```
when a website pulls a picture saved on the machine to display it
when a website pulls another file and displays it
the website is misconfigured and is allowed to serve any file on the server
```

#### LFI specific techniques

[hacktricks  |  everything LFI](https://book.hacktricks.xyz/pentesting-web/file-inclusion)

```
/proc/self/cwd/KNOWN_FILE	; for dealing with unknown path, but known dir contents
```


##### filters

Filters can be used to bypass limitations, such as a website executing the PHP code we are attempting to extract.

```php
php://filter/convert.base64-encode/resource=PATH_TO_FILE 	
```

The potential here is really spectacular, compressions filters such as `zlib.deflate` are particularly interesting.


##### fuzzing for filesystem readables

Once an LFI is identified, we can discover file system content via fuzzing. Here is a notable wordlist, deliver with your preferred tool:

```cmd
/usr/share/wordlists/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt
```


##### leverage /proc file system

The `/proc` file system, specifically the `/proc/self/` directory allows for a lot of creative results, here is a brief list of my favorites I have encountered so far.

```txt
/proc/self/cwd/FILE_WE_KNOW_EXISTS
/proc/self/cmdline  # cmdline
/proc/self/environ  # environment vars
/proc/net/tcp       # budget netstat
/proc/sched_debug   # running process and services
/proc/PID/maps      # replace process id, access virt address for binary exploit
```

If these fail, consider adding the header `'Range: bytes=200-1000'`. I have frequently been advised that this solves some `/proc` LFI failures, specifically `/proc/self/environ`, but I have yet to experience this behavior myself. 

A note on `/proc/self/cwd`. It can be useful for jumping into `vhost`'d websites if we leverage relative path traversal. 