## sed (stream editor) Cheat Sheet

- [Ranges](#ranges)
  * [Viewing a range of lines of a document](#viewing-a-range-of-lines-of-a-document)
  * [Exclude a range of lines of a document](#exclude-a-range-of-lines-of-a-document)
- [Replacing](#replacing)
  * [Replacing words or characters (basic substitution)](#replacing-words-or-characters--basic-substitution-)
  * [Replacing words or characters inside a range](#replacing-words-or-characters-inside-a-range)
  * [Replacing words only if a separate match is found](#replacing-words-only-if-a-separate-match-is-found)
- [Regular expressions](#regular-expressions)
  * [Using regular expressions (advanced substitution)](#using-regular-expressions--advanced-substitution-)
- [Editing and backing up files](#editing-and-backing-up-files)
  * [In-place editing and backing up original file](#in-place-editing-and-backing-up-original-file)
  * [Switching pairs of words](#switching-pairs-of-words)
- [Working with files](#working-with-files)
  * [Rename files inside a directory](#rename-files-inside-a-directory)
  * [Rename Strings inside files inside a directory](#rename-strings-inside-files-inside-a-directory)


## Ranges

### Viewing a range of lines of a document
To return lines 10 through 20 from a file, do:
```
sed -n '10,20p' file.txt
```

### Exclude a range of lines of a document
To exclude lines 40 through 60 from a file, do:
```
sed '40,60d' file.txt
```
## Replacing

### Replacing words or characters (basic substitution)
file.txt:
```
Hallo small thing
Welt is big
```
To replace words or characters from a file, do:
```
sed 's/small/BIG/g' file.txt
```
Output:
```
Hallo BIG thing
Welt is big
```

### Replacing words or characters inside a range
To replace words or characters within a line range from 10 through 20, do:
```
sed '10,20 s/small/BIG/g' file.txt
```
### Replacing words only if a separate match is found
file.txt:
```
my friend torben says hello
max also says hello
```
To replace the word hello with thanks only if the word friend is found, do:
```
sed '/friend/ s/hello/thanks/g' file1.txt
```
Output:
```
my friend torben says thanks
max also says hello
```


## Regular expressions

### Using regular expressions (advanced substitution)
To replace all spaces with an hyphen, do:
```
sed 's/\s/-/g' file.txt
```

## Editing and backing up files

### In-place editing and backing up original file
To replace all spaces with an hyphen inside a file and create a backup, do:
```
sed -i'.orig' 's/\s/-/g' file.txt
```

### Switching pairs of words
file.txt
```
Mustermann, Max
Becker, Boris
```
To switch the last name with the first name, do:
```
sed 's/\([^,]*\),\s*\(.*\)/\2 - \1/g' file.txt
```
Use `-r` option to make sed to use **extended regular expression**:
```
sed -r 's/([^,]+),\s+(.*)/\2 - \1/g' file.txt
```
Output:
```
Max - Mustermann
Boris - Becker
```

## Working with files

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
## Authors

* **Patrick Kowalik** - *Initial work* - [Sed CheatSheet](https://github.com/patrick0585/CheatSheets)
