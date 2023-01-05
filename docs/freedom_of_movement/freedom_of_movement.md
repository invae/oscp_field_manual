# freedom of movement

## less command

> for dealing with text wrapping/color codes issues from linpeas
```
less -S 	; deals with line wrapping
less -r		; deals with color issues
```

## ssh
> access the ssh command & ssh commands
```
~C   										; to enter the 'command' prompt
-L  local_port:127.0.0.1:remote port 		; tunnels our traffic through ssh to access a service running on target localhost
```


## text mangling/searching linux

> grep
```
grep -A4 -B4   				; show context lines 4 before and 4 after (example)

grep -v '/proc\|sys\|run' 	; select things which do NOT have {proc,sys,run}; notice we escape the | to get the 'or' sense

grep -oP "http://[A-z]"     ; pattern, only output match. non-useful example

grep -l                     ; output filenames instead of matchstrings
grep -f                     ; get patterns froma file, 1 per line
```

> find
```
has an -ls flag  			; changes output format to look tabular, like ls
```

> cut vs awk
```
use awk as often as possible; valuable tool; must get better at this
```




## MSF Framework

> searchsploit basics
```
searchsploit SEARCH_TERM		; search the local exploitDB
searchsploit -x PATH			; examine an exploit
serachsploit -m PATH			; make a copy of the exploit in current dir
```


## searching a filesystem

> windows powershell, recreating linux find, PS output is always an object, these are SLOW commands
```
get-childitem | where-object -property PROP_NAME -imatch SEARCH_TERM
get-childitem | select-string -pattern SEARCH_TERM
Get-ChildItem -Force -ErrorAction SilentlyContinue -Recurse -Path C:\* | FILTERING
	where-object -property PROP_NAME -imatch  SEARCH_TERM			; only checks file names
	or
	select-string -pattern SEARCH_TERM								; checks file contents as well
```

> windows cmd.exe
```
findstr /c: "Pattern" *.md  		; finds 'Pattern' in all .md files in the directory
```

## interacting with archives

> types of archives
```sh
docx
vhd 		; yes really
zip, tar, gz 
war  		; archive associated with tomcat website, contains a .jsp file which is like the php of a php site, its the scripting file
```

> list archive contents without opening / without pass
```sh
7z l *.vhd 		; lists contents of the virtual hardrive archive, works for any type
```


## dealing with heavy syntax

> js can be beautified
```
in web browser js tab
web apps accross internet ( BECAREFUL - NO SENSITIVE DATA)
```

> json
```sh
jq tool  # very useful commandline tool for beautifying/dealing with json returned from APIs
```


## no text editor available

Use the `grep` and `sed` method. This can be explained in roughly 2 steps.

1. use `grep -n` to output the line number, `x`, of whatever your pattern matches
2. use `sed 'xs/FIND/REPLACE/'`, to make modifications. Note that `x` is the integer found in step1

This works because `sed` is a line based text mangler. 
