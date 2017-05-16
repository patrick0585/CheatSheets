## [awk](https://de.wikipedia.org/wiki/Awk) Cheat Sheet

### Variables in awk
```
echo Hallo Welt  | awk '{printf "%s, %s!\n",$1,$2}'
```
Output:
```
Hallo, Welt!
```
### Get PID from a Process

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

