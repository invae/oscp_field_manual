# ftp specific movements

> recursively download an ftp server
```sh
wget -m --no-passive ftp://USER_NAME:PASSWORD@$ip
```

> alternatively if you are in console, it is similar to SMB
```cmd
prompt OFF
recurse ON
mget *
```
