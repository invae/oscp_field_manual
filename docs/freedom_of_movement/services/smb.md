# smb specific movements

> PSEXEC.py and SMB are related; think one see the other


## download an entire share recursively

### paste

> be on share root & make a local dir to catch the garbage
```cmd
recurse ON
prompt OFF
mget *
```

### explanation

```sh
smbclient //$ip//SHARE_NAME -U USER_NAME -P PASSWORD
smb> Recurse ON
smb> Prompt OFF
smb> mget *  		; on share root
```


## display windows extended attributes 

> filestreams, hidden, etc

```sh
smb> allinfo FILE_NAME
smb> dir /ah             ; dir attribute hidden
```






