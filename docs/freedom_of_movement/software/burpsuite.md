# burpsuite 

- hotkeys
- features
- tricks

## intercept everything

### cmdline http traffic

In bash the env var `http_proxy` will cause any http traffic of your child processes to pass through the proxy you specify.

```bash
export http_proxy 127.0.0.1:8080
# or wherever you have burp setup to listen
```

This is particularly useful for troubleshooting exploits and scripts. 


## repeater

- post requests have less bad characters


> URL ENCODE/DECODE HOTKEY
```
CTRL+U
CTRL+SHIFT+U
```

> to send a request in repeater
```
CTRL+SPACE
```

## intruder

> many attack types; notably clusterbomb/pitchfork
```
i mention pitchfork b.c it allows us to use multiple wordlists

also allows for the option to REGEXP inside response to get some updated value
	an alternate solution to what MACROS can provide
```


## macros

A larger topic, useful for repeating sequences of commands.

> example use case
```
site has CSRF protections and uses session tokens

each login attempt requires that we get a new
	session cookie
	CSRF protection token

otherwise our login attempt will not even get processes

macros solve this issue
macro will
	issue get request between each attempt
	get token and get cookie
	update token/cookie in next brute attempt

```


