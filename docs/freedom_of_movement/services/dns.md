# DNS

## Get TXT records

```bash
dig subdomain.domain.topleveldomain txt
```

```bash
nslookup -type=txt subdomain.domain.topleveldomain
```

## Tools for Exfil/Infil

- [packety.py] (https://github.com/kleosdc/dns-exfil-infil/blob/main/packety.py)
- [packetGrabber.py] (https://github.com/kleosdc/dns-exfil-infil/blob/main/packetyGrabber.py)

The packetGrabber.py is useful for reassembling an exfiltration. Given a domain and a pcap file, packetGrabber.py reassembles the output of a DNS exfiltration. Expects base58 encoded as base64, might not support other encodings. 


