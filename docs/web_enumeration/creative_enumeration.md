# creative enumeration methods
- `curl -v URL` as an enumeration tool; somtimes the site hides versions under popups (or is just not present in browser or source)
- `netcat` for fingerprinting; can sometimes grab the banner for further research
	- `nc -z`            zero-I/O mode used for scanning
- python or php server to receive CSRF proofs


## local enumeration of remote site
> best for use against small sites; download the entire site!
```sh
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://TARGET
```

> this one works for git folders
```shell
wget  -R "index.html*" --mirror --convert-links --no-parent http://siteisup.htb/dev/.git/
```
idk if convert-links is necessary; note there is a lot of redundancy in these flags.

## fuzzing
> with FFUF
```
syntax is a bit easier than wfuzz
note the content type
note the cookies 	
note the headers	

common flags:
	-H 'Name: Value'						; accept multiple
	-x POST  default is GET
	-d 'POST DATA'
	-c colored output
	-b "NAME1=VALUE1; NAME2=VALUE2" 		; cookie data
example: 

ffuf -w /path/to/wordlist -u https://target/FUZZ

```

## XSS cookie stealing

> host a malicious js; attempts to steal cookie
```js
script will contain something like:
	document.Write('...'+doc...cookie...)

/*
writes victim cookie into web request, cookie visible in 'GET request' / 'web server log'
*/
```

