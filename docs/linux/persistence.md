# persistence

## basic & noisy

> suid copy of `/bin/bash`

- in {target we will escalate to}'s home directory (or anywhere perhaps the /dev or /tmp )
- has suid set
- other group has x permision
- when executing, use -p flag to keep permissions


> create .ssh/authorized_keys & add my pub_key enables `ssh@$IP -i id_rsa` 

- create a new key with `ssh-keygen -f NAME -c 'invae'`; chmod as necessary; copy to victim
- keys behave best with permission 600
- perm 700 for .ssh (owner of home dir owns .ssh not root)
- perm 644 for authorized_keys, 1 key per line
- perm 644 for a pub_key 
- private key DOES NOT go on the target; but perm 600 for id_rsa
- home directory is usally at most perm 755