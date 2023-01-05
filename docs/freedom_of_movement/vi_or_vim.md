# vi_or_vim

## essentials

> open the vi prompt; this is for entering meta commands
```bash
:
# note the prompt has history
# navigate with arrowkeys after entering
```


> how to escape; close the tool
```bash
:
q
# note that ! or w might be required
# ! is for force
# w is for write
```


> moving the cursor; `arrow keys` or `h`, `j`, `k`, `l`
```bash
# self explanatory
arrow keys
# these feel a bit constricted to me
h # left
j # down
k # up
l # right
```


> enter `insert` mode
```bash
# move cursor into position
i
```


> exit any `mode`, such as `copy`, `insert`, `visual` , etc
```bash
# spam the ESC key
# at least one press is necessary
```


> searching simlar to `less`, similar rules apply
```bash
# start searching, then input your pattern
# search is performed top of document downwards
/ 
# we observe some highlighting, usually YELLOW
# the editor will jump to first result
# 
# Jump to next result
n
```


## advanced concepts

> deletions; lines, words
```bash
# move cursor onto begining of the object
#
dw # delete word
dd # delete line
# periodic writes and backups are advised
# latency and learning can cause errors
```


> jump to insert mode, in the line below cursor location
```bash
o
```


> copy; ***YANK***, yank an entire line
```bash
yy
```


> paste; paste the entire line, below the line the cursor is on
```bash
p
```


> search and replace with `sed` inside `vi`/`vim`
```bash
# enter the vi prompt
:
# in the vi prompt we use this to start a sed command
%s
# enter our sed command
# e.g. of what is commonly required
%s/SEARCH_TERM/REPLACE_TERM/gi
# the trailing /gi is for 
# g - global
# i - insensitve
# excellent because it nearly identical to common regex implementations
#
# this can be extended to regex for anything
# including special chars; e.g. replacing \n with CATS
%s/\n/CATS/g
#
# search current line only, replace first occurence
# once again in the : prompt
.s/SEARCH/REPLACE/
# . - indicates current line
# add the g suffix to search/replace whole line
# add the i suffix to search ignoring case
``` 