## sed (stream editor) Cheat Sheet

### Rename files inside a directory
Directory:
```
file1
file2
file3
file4
file5
...
```
with the following command all files will be renamed
```
 for i in $(ls); do (mv "$i" "${i/file/hallo}"); done
```
After:
```
hallo1
hallo2
hallo3
...
```

### Rename Strings inside files inside a directory
Files:
```
abc.txt
   >blah
   Hallo Welt
   ...
abc1.txt
   >blahblah
   Hallo 123 Welt
   ...
...
```
Command:
```
for file in *.txt; do (sed -i.bak 's/>.*/REPLACESTRING/g' $file); done
```
Output Files:
```
abc.txt
   REPLACESTRING
   Hallo Welt
   ...
abc1.txt
   REPLACESTRING
   Hallo 123 Welt
   ...
...
```
