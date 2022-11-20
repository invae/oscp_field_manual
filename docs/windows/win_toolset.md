# win_toolset

> tools for attacking windows
```
responder.py 			; trick victim into reaching out to me, victim tries auth via hash, responder captures hash
psexec.py 				; a possible shell, not available for all groups, smb related
evil-winrm				; port 5985 or win rm service must be running
```

> smbclient ; not a pentesting tool
```
smbclient -U '' -P '' //$ip/SHARE   	; is NULL authentication
smbclient -L //$ip 						; is list shares
```

> crackmapexec 	; sharing services swiss army knife ?
```
enumerate all kinds of services
frequently used for FTP
privided with creds it will verify and return to me what is writable/readable

tool is for
	enumeration
	bruteforce
	access (shells)

more experience with this tool is necessary, its a huge toolbox
```

> the entire IMPACKET library; located in my opt directory b.c my first install was bad; checkout EXAMPLES folder
```sh
this entire library has excellent tools for acheiving our goals
too much to describe

highlights
	SMBServer.py
		host smb server on my attacking linux vm to send files to attacking windows for further analysis
		see -h for host setup
		on windows:  win+r \\HOST_IP\SHARENAME to access share
	Get-AD-users.py
		tool for bruteforcing RIDs to enumerate AD users
	secretsdump.py
		alternative to mimikatz? same idea, dump hashes from SAM once you have a system acc
		first harvest hashes via
			"reg save HKLM\system"
			"reg save HKLM\sam"
```




