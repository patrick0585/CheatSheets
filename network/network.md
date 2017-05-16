# unix network commands Cheat Sheet

#### search for available ip adresses inside a subnet
```
for i in {1..254}; do (ping 192.168.178.$i -c 1 -W 1 >/dev/null && echo "192.168.178.$i"); done
```
Result:
```
192.168.178.20
192.168.178.29
```

#### retrieve ip address from a hostname
```
nslookup www.google.de | awk -F': ' 'NR==6 {print $2} '
```

#### retrieve every ip address from a list with hostnames
```
File: test.txt
--------------
www.google.com
...
--------------
```
```
for hostname in `cat test.txt`; do (nslookup $hostname | awk -F': ' 'NR==6 {print $2} '); done
```

#### list all open ports
```
netstat -lntup
```
    . -l = only services which are listening on some port
    . -n = show port number, don't try to resolve the service name
    . -t = tcp ports
    . -u = udp ports
    . -p = name of the program

Result:
```
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:6379            0.0.0.0:*               LISTEN      3804/****
tcp        0      0 127.0.0.1:63342         0.0.0.0:*               LISTEN      2507/****       
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      -              
...
```
