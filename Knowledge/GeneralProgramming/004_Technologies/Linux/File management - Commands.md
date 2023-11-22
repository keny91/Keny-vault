

### LIST - ls

```
ls -(l a R h)
ll -(l a R h)
```


### Chown 


### Chmod
### pwd - path to current dir

```
pwd -( L -- display env, P -- Absolute path)
```

1. **cat** – list content of file to terminal
2. **clear** – clear terminal window
3. **echo** – move data into a file
4. **less** – used to read the contents of textfile
5. **man** – show manual of Linux commands
6. 1. **cd** – change directory
2. **mkdir** – make new directory
3. **mv** – move files / rename files
4. **cp** – copy files
5. **rm** – remove files
6. **touch** – create blank new file
7. **rmdir** – delete directory
8. 1. **head** – view first lines of any text file
9. **tail** – view last lines of any text file
10. **whereis** – used to locate the binary, source, manual page files
2. **whatis** – used to get one-line man page description
3. **useradd** – used to create a new user
4. **passwd** – used to changing password of current user
5. **whoami** – print current user
6. **uptime** – print current time when machine starts
7. **free** – print free disk space info
8. **history** – print used commands history
9. **uname** – print detailed information about your Linux system
10. **ping** – to check connectivity status to a server
11. **chmod** – to change permissions of files and directories
12. **chown** – to change ownership of files and directories
13. **find** – using find searches for files and directories
14. **locate** – used to locate a file, just like the search command in Windows
15. **ifconfig** – print ip address stuff
16. **ip a** – similar to ifconfig but shortest print
17. **finger** – gives you a short dump of info about a user


### grep

```
grep [OPTION...] PATTERNS [FILE...]

cat sample | grep -v a | sort - r
```

**-c** : This prints only a count of the lines that match a pattern
**-h :** Display the matched lines, but do not display the filenames.
**-i :** Ignores, case for matching
**-l :** Displays list of a filenames only.
**-n :** Display the matched lines and their line numbers.
**-v :** This prints out all the lines that do not matches the pattern
**-e exp :** Specifies expression with this option. Can use multiple times.
**-f file :** Takes patterns from file, one per line.
**-E :** Treats pattern as an extended regular expression (ERE)
**-w :** Match whole word
**-o :** Print only the matched parts of a matching line,
 with each such part on a separate output line.
 

**-A n** **:** Prints searched line and nlines after the result.
**-B n :** Prints searched line and n line before the result.
**-C n :** Prints searched line and n lines after before the result.

![[Grep 1.png]]


### sort

