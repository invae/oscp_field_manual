# msfconsole

This section contains interesting quirks/tricks to the msfconsole. May include some basic usage guides. 


## issues with process migration

The case study is the exploit suggester for Windows targets. The suggester should be run in both 32 bit and 64 bit modules, as the results may differ. The attack surface will be the union of the sets of the outputs. 

> migration from 32 to 64 may cause subsequent exploits to fail, silently, or with minimal feedback. Process migration is appropriate if attempting to avoid detection or if exploit suggester module is not necessary. Migrating to a process of the same architecture is advised. 


Example workflow, full enumeration

1. Catch a 32 bit meterpreter shell
2. Run 32 bit suggester via 32 bit meterpreter shell
3. Catch a 64 bit meterpreter shell, we now have **two** distinct sessions
4. run 64 bit suggester via meterpreter shell
5. Analyze the suggested attack surface 
6. Run exploits in the according 32 or 64 bit sessions

Opsec to be considered 

- additional noise in the process tree of multiple sessions
- more disk traces to clean up, we have a 32 and 64 bit agent present


## get pretty/extended exploit info

Use this command to generate a `.HTML` doc in `/tmp` for nicer, more detailed viewing

```cmd
info -d 
```

## enable pivoting

### socks4 and proxychains

Metasploit has a socks_proxy server function, which enables for easy routing of our traffic through our agents.

#### setup

First we must define some routes, the general syntax is

```cmd
route ADD/DEL IP_ADDR/SUBNET_CIDR SESSION_TO_ROUTE_THROUGH
```


Example routes

```cmd
route add 172.17.0.1/32 -1
route add 172.28.101.51/32 -1
route print
```

Once routes are set, we can start the service. Note the `version=4a`

```cmd
use auxiliary/server/socks_proxy
auxiliary(server/socks_proxy) > run srvhost=127.0.0.1 srvport=9050 version=4a
```


#### example usage

> in msfconsole. Note server must be running and route defined. 
```cmd
msf6 auxiliary(scanner/ssh/ssh_login) > run ssh://USERNAME:PASSWORD@172.17.0.1   
```

> on command line tools
```cmd
curl --proxy socks4a://localhost:9050 http://172.17.0.1 -v
```

> make sure `/etc/proxchains.conf` is set to v4 not v5!
```cmd
proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 172.17.0.1
```

```cmd
proxychains ssh USERNAME@172.17.0.1   
```
