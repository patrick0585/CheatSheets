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
