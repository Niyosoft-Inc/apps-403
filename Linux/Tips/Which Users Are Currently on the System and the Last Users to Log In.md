Command Line Basics

## Determine the Current Working Directory

Use the following command to determine the current working directory:
```
pwd
```
Change your working directory to your user's home directory.
```
cd ~
```
Verify that we are now in the /home/cloud_user directory.
```
pwd
```


## Determine Which Users Are Currently on the System and the Last Users to Log In

Determine if any other users are currently logged in to the system.
```
w
```

Determine which users last logged in to the system and when the system was last booted.
```
last
```

Record Your Findings in /home/cloud_user

Write the output of the previous commands into a new file in the cloud_user home directory.
```
w > log.txt
last >> log.txt
```

View the contents of the file we just created.
```
cat log.txt
```
