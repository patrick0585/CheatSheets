## [perl](https://de.wikipedia.org/wiki/Perl) Cheat Sheet

### Remove strings inside a certain file
**File-Input:**
```
Hallo
Welt
```
**Command:**
```
perl -i -pe 's/Hallo/blah/' dump.txt
```
**Output:**
```
blah
Welt
```
**Command-Options:**
* **-i** : this writes the converted input back to the original file
* **-p** : this loops round all the lines in the file. Each one, in turn, is stored in ```$_``` and the contents of ```$_``` are printed after each iteration of the loop.
* **-e** : this is the code you want to run for each line of the file.

### Remove string inside file of a certain type
**Command:**
```
find . -name "*.txt" -exec perl -i -pe 's/ABC/1111/' {} \
```
