# general firewall evasion tactics
- encode the payload (for pwsh -enc command or b64 -d)
- try funny port
- try normal ports
- ipv6 to evade lazy filtering rules



## encoding payloads for windows
> when encoding before base64 ing the payload; allows `pwsh -enc PAYLOAD`
```sh
iconv -t UTF-16LE
```

