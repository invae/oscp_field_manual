# burpsuite 
- hotkeys
- features
- tricks


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
a larger topic
useful for repeating sequences of commands

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


