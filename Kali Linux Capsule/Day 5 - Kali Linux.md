##### Grep command
`grep` command is used to search and display lines matching a pattern in files or input.
```
grep "error" file.txt
grep -i "linux" file.txt
ps aux | grep root
```

##### egrep command
`egrep` searches text using extended regular expressions and is equivalent to `grep -E`
```
egrep "error|fail" log.txt
egrep "(cat|dog)" file.txt
ps aux | egrep "root|admin"

```

##### fgrep command
`fgrep` searches for fixed (exact) strings and does not support regular expressions in Linux and is equivalent to `grep -F`.
```
fgrep "error.log" file.txt
fgrep "a+b" file.txt
ps aux | fgrep root
```
