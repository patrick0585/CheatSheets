## [awk](https://de.wikipedia.org/wiki/Awk) Cheat Sheet


- [usefull awk commands](#usefull-awk-commands)
  * [variables in awk](#variables-in-awk)
  * [get pid from a process](#get-pid-from-a-process)
  * [top 10 commands often used in history](#top-10-commands-often-used-in-history)



## usefull awk commands

### variables in awk
```
echo Hallo Welt  | awk '{printf "%s, %s!\n",$1,$2}'
```
Output:
```
Hallo, Welt!
```
### get pid from a process

```
ps -ef | grep redis
```

Output:
```
xxxxxx   5394  5243  0 Mai03 pts/4    00:11:53 redis-server *:6379
xxxxxx  20877 20835  0 08:13 pts/22   00:00:00 grep --color=auto redis
```
grep the process without the grep command
```
ps -ef | grep "[r]edis"
```
Output
```
xxxxxx   5394  5243  0 Mai03 pts/4    00:11:53 redis-server *:6379
```

get only the PID from the process
```
ps -ef | grep "[r]edis" | awk '{print $2}'
```
a better way without grep:
```
ps -ef | awk '/[r]edis/ {print $2}'
```
Output:
```
5394
```
### top 10 commands often used in history

command:
```
history | awk ‘{a[$2]++}END{for(i in a){print a[i] ” ” i}}’ | sort -rn | head
```
sort-information:

**-r, --reverse**

    reverse the result of comparisons
**-n, --numeric-sort**

    compare according to string numerical value

output:
```
191 cd
162 joe
161 ls
136 hg
...
```
