# Basic Enumeration of Linux 
Answer the following every time:

- who is this user?  -> enumerate the `/opt` directory !! search for files owned by the user
- what do they do/ what is their role?
- what do they NEED to do what they do ?

```
ls -Alh *             						; sneaky directory enumeration
.ssh										; upgrade access from webshell
```

> manual enumeration for priv esc
```
setup /dev/shm
find > something.txt
getcap -r /  > something.txt
```

> interesting locations upond landfall
```
w                                           ; who logged, what doing
id 											; group membership ?
.profile/.bash_history type files			; or user specific .conf
echo $ENV
/var/										; this is where users make their mistakes are such as /var/backups
/opt
/usr/local 									; out of date software goes here (not touched by pckg manager)
/etc/hosts
/etc/passwd
/etc/crontab
ss -lntp 									; tcp listeners on victim (enumerating services)
ps -ef 										; enumerate processes visble to me
```


## who uses this machine?
collect human profiles on the users as well; we want to know EVERYTHING
```bash
w        # who is logged on, what they are doing (better who)
last     # show list of last logged on users, invesitgate precedence
```


## permissions  
```
id   - take note of groups

find -type -f -perm -4000 -o -perm -2000	; get those SUID/GUID files
	information on directory containing user owned SUID/GUID file 
	if we can write here we can write symlink ontop of w.e has suid; e.g ln -sf BAD_SCRIPT.sh SUID_SCRIPT.sh  			; this is an escalation, move to new file

crontab -l/ crontab -e / read /etc/crontab

getcap -r / 2>/dev/null 					; can process set its UID set_uid cap, especially code on machines

etc/doas.conf 

sudo -l      								; (NOISY)
```

## notable group membership	

> adm group
```
Go and read all the system logs in /var/log and other locations
```

> ldx lxc containerd docker groups
```
attempt the alpine container priv esc
in general look for virtualization related vulns
```

> custom groupname ?
```
find -group CUSTOM_GROUPNAME 2>/dev/null
```




## geography & basis of reality
> host identity
```sh
hostname           ; give hostname
cat /etc/*rel*     ; give OS release info
```

> Which package managers are present?
```sh
snap
dpkg -l           ; # list packages
rpm  -qa          ; # query all
```

> PATH/ENV enumeration						; a bit more involved
```
'w' command 								
; gives information on signed in users and what they are doing

echo $PATH								; modify path to location of BADBINARY
echo $ENV								; this one may be wrong ?

--- no idea what the following is talking about ---
requires an elevated execution
requires a call to some other system binary	; strace command potentially useful
requires the binary call to be not full path qualified
The specifics vary a lot here; sometimes we replace a system binary; othertime a shared object
```

> SERVICES enumeration
```
find .service files							
; .service file is similar to .conf  rules/scripts to execute at startup, perms?
	common .service entry is ExecStart		
	; binary which occupies this value is exec at start, can hold a bash -c 'CMD'
	/usr/lib/systemd/system/
	/run/systemd/system/
	Do not directly edit the SERVICE file in the directory. 
	Instead, copy, edit, then override the original 

ps aux										; big info on  process/services
pe -ef --forest								; similar to aux but diff format; --forest flag works for aux

ss -lntpa 									
; show listening tcp ports, include processes

ls /proc									; lists running processes in the 
pseudo file system /proc

systemctl status SERVICE					
; pay attention to 'Loaded' category, similar to DLL, MakeFile, or .conf, we can perhaps hijack
Enumerate the loaded library!				
; enumerating these loaded libraries is essential, library perms?

netstat -ltp or netstat lntp ; BOOMER ss


```

> victim machine ports; local host
```
ss -tulpn
netstat -tulpn
ssh -L PORT:localhost:PORT -i id_rsa user@$ip 		; will forward traffic to my localhost, bypassing firewall, needs initial accesss
note id_rsa should be created on a per box basis 	; protect my local username
```


## information disclosure
```
.*history									; unintended info disclosure
.config										; unintended info disclosure
Network files and shares					; potential escallation/information
enumerate all /etc/*.conf files
e.g. /etc/resolv.conf <- get DNS info

Can i read /var/mail/* ??? 

pay attention to MOTD on login
```

## pattern recognition; environment analysis
> watching for changes and timestamps can be tedious when you mangle the syntax repeatedly
```sh
watch -n 1 ls -la /dev/shm
# will give an update of changes on the /dev/shm dir every minute
# REALLY powerful for monitoring for file creations; or just movement of crontjobs etc etc
# powerful for demonstrating proofs of your command executions
# powerful for demonstrating
# demonstrating
```


> novell methods of enumeration
```
lsof           ; list open files
```

## enumerating internal services
> common tools; likely to exist on target
```bash
ss -lntp 
netstat ano
ps -ef --forest
```

> forcing a tcp handshake and get data
```
nc -z           # zero-I/O mode [used for scanning]
curl
wget
```


## help, I am in a container
> investigate root for strange files or dirs such as
```
dockerenv
vbox
vmware
```

> /proc still exists, consider reading the following
```sh
/proc/net/tcp       # buget netstat
/proc/self          # traditional LFI file
/proc/sched_debug   # running process//services
/proc/PID/maps      # replace process id, access virt address for binary exploit
```
- these are also powerful when local file inclusion vulnerabilty is discovered.
- **unfamiliar output** should be googled, it is not being parsed by `netstat` so you must parse it yourself. see alternate expressions of ip address 



