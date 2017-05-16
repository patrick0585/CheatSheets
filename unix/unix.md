# basic unix commands Cheat Sheet

## Loops

### For sample
```
for f in $(ls); do (echo $f); done
```

### C-like for
```
for i in `seq 1 10`; do (echo $i); done
```

## Time/Timestamp

### Get actual time
``` 
date
``` 
Output:
``` 
Mo 07. Mai 22:00:00 CEST 2017
``` 

### Format timestamp
``` 
date +"<parameter>
``` 
Available parameter:
``` 
%T  - 22:00:00        time
%Y  - 2017            year
%m  - 05              month
%d  - 07              day
...
``` 

