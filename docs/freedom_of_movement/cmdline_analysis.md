# cmdline_analysis

> tricks & techninques for analyzing folders, volumes, source codes via cmd line

## hashing algs

Hashing algs can be used to identify unique files inside a directory.

1. compile lists of md5sums of each file in dir (assuming multiple trees)
2. use diff -y TREE_SUMS_A TREE_SUMS_B to compare
	1. lists must be sorted
3. the goal is to find **unique** md5sums between the two trees


## specific tools

### diff
tool made to show differences between files
> e.g. side by side comparison
```sh
diff -y file_a file_b | less -S
```

### watch
tool mad to update STDOUT based on an interval
> e.g. monitor a directory for changes every second
```bash
watch -n 1 ls -al /dev/shm
```

