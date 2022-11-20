# smb specific movements

> PSEXEC.py and SMB are related; think one see the other


> display windows extended attributes (filestreams etc)
```sh
smb> allinfo FILE_NAME
```

> download an entire share recursively
```sh
smbclient //$ip//SHARE_NAME -U USER_NAME -P PASSWORD
smb> Recurse ON
smb> Prompt OFF
smb> mget *  		; on share root
```


