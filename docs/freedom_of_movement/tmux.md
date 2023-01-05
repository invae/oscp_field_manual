# tmux

## basic conf file

> for less psychotic keybinds; place in  `~/.tmux.conf`; new prefix is `CTRL a`
```cmd
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
set-option -g default-shell /bin/zsh
set -g history-limit 9001
```

## tmux essentials

> if you are ever lost in your tmux session, you can list all windows in pane in a GUI, which provides a preview of what is on each window and pane.
```cmd
PREFIX w
```


> searching tmux history; works in broken/scuffed shells
```
PREFIX [					; enters 'copy mode', allows for searching text
CTRL+S 						; search down, from begining of history to present
# alternatively...
CTRL+R 						; search 'reverse' from present backwards, preffered
CTRL+SPACE 					; start highlighting text in copy mode
CTRL+W 						; copy highlighted text
prefix ]                    ; paste the copied text
```


> create window; rename window; go to last window; go to window number `X`, where `X` is an integer
```cmd
PREFIX c
PREFIX ,
PREFIX l       ; note this is a lowercase L
PREFIX X
```



> kill current pane; may be `TTY` specific, see `stty -a` to see how signals are bound
```
CTRL+D 						; just like a python REPL- read evaluate print loop
```


## tmux meta-session commands

### tmux prompt 

Almost all of the cmdline actions we can do such as `tmux ls` work inside the tmux prompt.

> enter via 
```cmd
PREFIX SHIFT :
```


> modify tmux session home; first enter the tmux prompt
```cmd
attach -c /path/to/new/home 
```


> rename a window
```cmd
rename-window NEW_NAME
```


### tmux administrative commands

> rename session
```cmd
PREFIX $
```


### tmux scripting

Powerful for repeated tasks such as setting up a workspace for attacking an single target. Possible to create initial workspace directory structure, set environment variables specific to a tmux session and stage initial recon commands. 

> example; note `C-m` is the way tmux scripting sends `Enter` to a session
```cmd
tmux send-keys 'sudo nmap -v -sC -sV 8.8.8.8 -oA first_scan' C-m
```

> run a script on a tmux pane via
```bash
# begin by selecting the pane of interest
# next, enter the tmux prompt
PREFIX :
# finally, we run the script we have prepared
run-shell ~/PATH/TO/SCRIPT
```



## references

1. [run-shell discovery](https://superuser.com/questions/827816/create-custom-command-in-tmux)
2. [tmux reference via short youtube vids](https://www.youtube.com/playlist?list=PLTRNG6WIHETB4reAxbWza3CZeP9KL6Bkr)