# proof of concept

often when trouble shooting exploits we must understand syntax specific to some programming language

## vulnerability specific tips
> When doing research on specific protocols consult:
```sh
RFC/IETF 			# internet engineering task force
# usually have excellent whitepapers giving info needed
```



## command execution

> If you control config files, you can likely get command execution

Try the most base, elemental, features of command execution; such as id, ping etc. 

Ping + tcmpdump icmp is especially good for blind/limited feedback RCE!!


## language specific tips
### python
> interactive mode
```python
python -i exploit.py 			; runs script in interactive mode, interprets all lines then maintains so u can interact
```

> similar to interactive mode, the python debugger allows for understanding of other code & powerful troubleshooting	 
```python
import pdb

pdb.set_trace()  	# like a breakpoint

# after doing the exec the python script and it will drop you into pdb where gdb like commands can be used to query values
# reference
# https://www.youtube.com/watch?v=qECG2_8xw_s&t=1740s&ab_channel=IppSec
```

> list all object attributes
```
dir([object]) 		; list all attributes in an object, get info about the object recursively
dir(None)			; returns names in current scope
```

> debugging
```python
print(my_var)
input()
or
print(f'{my_var=}')  ; note that we can put all kinds of expressions in here
input
```

> requests library; dealing with large DATA use the docstring! it is a multiline literal string
```python
data = """ HEADER """
```

> nice aesthetic rolling text
```python
import sys

sys.stdout.write( f"..." ) # creates some nice rolling text due
sys.stdout.flush()         # do this when done to clear the write buffer
```

### php
> interactive mode
```php
php -a		
// opens an interactive session for doing tests, similar to python REPL
```

