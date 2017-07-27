## basic unix commands Cheat Sheet

- [Loops](#loops)
  * [For sample](#for-sample)
  * [C-like for](#c-like-for)
- [Time/Timestamp](#time-timestamp)
  * [Get actual time](#get-actual-time)
  * [Format timestamp](#format-timestamp)
- [Disk Free](#disk-free)
  * [Freien Speicherplatz des gesamten Dateisystems anzeigen](#freien-speicherplatz-des-gesamten-dateisystems-anzeigen)
  * [Freien Speicherplatz des lokalen Dateisystems anzeigen](#freien-speicherplatz-des-lokalen-dateisystems-anzeigen)
- [Disk Usage](#disk-usage)
  * [Gesamten belegten Speicherplatz des Systems anzeigen](#gesamten-belegten-speicherplatz-des-systems-anzeigen)
  * [Belegten Speicherplatz des Ordners Media anzeigen, ohne *.bmp Dateien zu berücksichtigen](#belegten-speicherplatz-des-ordners-media-anzeigen--ohne--bmp-dateien-zu-ber-cksichtigen)
  * [Belegten Speicherplatz des aktuellen Verzeichnisses anzeigen](#belegten-speicherplatz-des-aktuellen-verzeichnisses-anzeigen)
  * [Sortierung des belegenten Speicherplatz mit maximaler Rekursions-Tiefe von 1.](#sortierung-des-belegenten-speicherplatz-mit-maximaler-rekursions-tiefe-von-1)





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
## Disk Free
**disk free** zeigt den freien, also verfügbaren, Speicherplatz auf der Festplatte an
```
df
```
### Freien Speicherplatz des gesamten Dateisystems anzeigen
```
df -h
```
### Freien Speicherplatz des lokalen Dateisystems anzeigen
```
df -hl 
```

## Disk Usage
**disk usage** zeigt den belegten, nicht verfügbaren, Speicherplatz auf der Festplatte an

### Gesamten belegten Speicherplatz des Systems anzeigen
```
du -sh /
```
### Belegten Speicherplatz des Ordners Media anzeigen, ohne *.bmp Dateien zu berücksichtigen
```
du --exclude="*.bmp*" -sh media/ 
```
### Belegten Speicherplatz des aktuellen Verzeichnisses anzeigen
```
du -sh ./
```
### Sortierung des belegenten Speicherplatz mit maximaler Rekursions-Tiefe von 1.
```
du -h --max-depth 1 ./ | sort -h
```

