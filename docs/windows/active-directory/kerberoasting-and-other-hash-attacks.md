# kerberoasting-and-other-hash-attacks

## Creating Initial Userlists

If passive recon fails to populate userlists, then we can populate a userlist by bruteforcing RIDs. Try with all of the following:  `Guest` , `''` (NULL) , and `anonymous`  (non-existent user and any pass) authentication. 

```cmd
lookupsid.py Guest@$ip 
```

```cmd
lookupsid.py ''@$ip 
```


## Traditional Kerberoasting - Service Principal Names

Accounts with a "Service Principal Name", an SPN,  have the feature such that any member of the domain can request a service ticket for the account that has an SPN. These accounts are generally known as "service logon accounts". The presence of this SPN attribute results in us being able to request a service ticket, the hash, that can then be brute forced with hashcat in order to recover the password. The `Guest` account cannot ask for an SPN or list accounts which have an SPN. 

List Users with SPNs

```cmd
GetUserSPNs.py DOMAIN/USER:PASSWORD@$ip
```


Get the ticket associated to an SPN

```cmd
GetSPN.py -h
```


Here is a list of nice reads or viewings on the topic

- [risk3sixty | explain SPN kerberoasting](https://risk3sixty.com/2022/10/10/understanding-kerberoasting/)


## AS REP Roasting - No PreAuthentication Required 

AS REP Roasting is an offline brute force attack on the AS Reply hash provided by the Kerberos Protocol. In order to request an AS Reply hash for a user, the AD user must have the "PreAuthentication not required" trait. This trait is ***extremely*** uncommon in the wild. However, it exists and may be implemented in the AD networks we are interested in. 

```cmd
GetNPUsers.py DOMAIN -usersfile USERS.LIST -no-pass -dc-ip $ip
```

Here is a list of nice reads or viewings on the topic

- [kerberos pre-auth | VbScrub - youtube](https://www.youtube.com/watch?v=pZSyGRjHNO4&ab_channel=VbScrub)


## Pass the Hash 

Generally the "post exploitation" of a successful `secretdump.py` or other `mimikatz` like dumping of creds from Local Security Authority Subsystem `lsass.exe` process, Security Accounts Manager `SAM`, Credential manager `CredMan`, or even `ntds.dit` database. 

- The resulting hashes can be used to spray across the environment for further access.
- Hash-based authentication like this is not always possible, it can be explicitly disabled.
- Alternatively, if username/password authentication fails, hash based authentication should be attempted too in order to cover edge cases. User-pass disabled, hash enabled.

```cmd
wmiexec.py -hashes LM-HASH:NTLM-HASH USER@$ip
```

Other tools which enable hash-based authentication attempts

- `smbexec.py`
- `evil-winrm`
- `crackmapexec`


## Silver Tickets - under construction

This is usually "post exploitation" of a successful initial kerberoast. We can use the password looted from a successful roast of a hash, compute the NTLM of that pass, get the Domain SID (it is prefix to a user SID), then we can get our silver ticket. 

services generally vulnerable to silver ticket attacks

- mssql service


## Golden Tickets - under construction

I have awareness of this but cannot explain it at this time ...


## External Cheatsheets & Lists

- [kerberos cheatsheet  | TarlogicSecurity](https://gist.github.com/TarlogicSecurity/2f221924fef8c14a1d8e29f3cb5c5c4a)
