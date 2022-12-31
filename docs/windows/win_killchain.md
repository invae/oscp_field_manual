# win_killchain 
- identify target is windows
- identify vuln
- weaponize the vuln
- exploit / detonate the weapon
- Initial Access
- System/Administrator Group (Required for Hashdumping)
- mimkatz
- dump hashes (via reg save or mimikatz; then dump locally)
- horizontal escallation/pivot


## claim some territory

> world writable
```
%AppData%
usually is C:\Users\USER_NAME\AppData\Roaming

C:\windows\tasks

C:\temp
```

