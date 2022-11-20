# The Find Command

## overview

> linux find command frequent useful commands
```shell
find LOCATION -type f -iname PATTERN -perm -2000 -o -4000 2>/dev/null
other logics possible such as:
	-a 										; AND operator
	-o										; OR operator
	-perm /u=s 				; files with suid bit active
	-exec CMD {} \;			; {} is the output of find, similar to piping, one per line
	-exec CMD {} \+							; concatenates output, results in 1 cmd being exec instead of each
	considering piping into xargs -p -n 	; for prompt && 1 per line
```

## leverage timestamps
> aka bookend search; time period search; newer modified time
```shell
find / -newermt "YYYY-mm-dd" -newermt "YYYY-mm-dd" 2>/dev/null -ls
```


## lazy ls
> list a dir, recursively; possibly the best flag
```shell
find . -ls 2>/dev/nulll
```

## permission bits
> the classic
```shell
find / -type f -perm -2000 -o -perm -4000 2>/dev/null 		; note the - prefix on the perm_num, this means "at least"
```

## users, groups, attributes
> targeted enumeration; lateral movement

```shell
find / -group GROUP_NAME
```

```shell
find / -user USER_NAME
```

```shell
find . -writeable   
```


