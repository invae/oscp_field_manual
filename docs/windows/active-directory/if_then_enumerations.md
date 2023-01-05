
# if_then_enumerations

## Can Read Netlogon and Sysvol

If can read Netlogon and Sysvol then run `bloodhound.py`

```bash
python3 bloodhound.py --dns-tcp -ns $ip -d target.com -u 'USER' -p 'PASSWORD'
```

Note that all variations such as `target.com` , `dc.target.com`,  and `dc01.target.com` must be added to the `/etc/hosts` to avoid issues with the impacket library. ***Pay attention*** to this step, errors can cause severe loss of time. 


