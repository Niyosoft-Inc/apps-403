## Using Directories and Listing Files

Determine Which File Is the Oldest
Determine the current working directory.
```
pwd
```
List the contents of the current working directory.
```
ls
```
Change to the Practice folder.
```
cd Practice/
```
List the contents of the Practice folder.
```
ls
```
Change to the Test folder.
```
cd Test/
```
Open the man page for the ls command.
```
man ls
```
Locate the entry for the -l option, and read the description.
Locate the entry for the -A option, and read the description.
Locate the entry for the -t option, and read the description.
Run the following command to determine the oldest file:
```
ls -lAt ~/Practice/Test/var/log/
```


### Determine Which File Is the Largest
Open the man page for the ls command.
```
man ls
```
Locate the entry for the -S option, and read the description.
Run the following command to determine the largest file:
```
ls -lS ~/Practice/Test/var/log/
```


### Determine When the File ```~/Practice/Test/sos_commands/networking/netstat_-W_-neopa``` Was Last Modified
Run the following command:
ls -l ~/Practice/Test/sos_commands/networking/netstat_-W_-neopa


### Determine When the File `~/Practice/Test/sos_commands/networking/netstat_-W_-neopa` Was Last Accessed

Open the man page for the ls command.
```
man ls
```
Locate the entry for the `-u` option, and read the description.
Run the following command to determine when the file was last accessed:
```
ls -lu ~/Practice/Test/sos_commands/networking/netstat_-W_-neopa
```
Check the current date to confirm.
```
date
```

