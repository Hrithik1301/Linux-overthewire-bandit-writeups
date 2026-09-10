
Connecting to ssh level 2 using the credentials from Prv level

ssh bandit2@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html)

after logging in, used "cat ./--spaces in this filename--" cmd, bcos it worked prvly for a file name"-"

but the following errors occured

cat ./--spaces in this filename--
cat: ./--spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename--: No such file or directory

upon asking claude, and asking me to brief about the info. in the url provided in the webpage about the usage of spaces it gave the following info. 

The terminal treats spaces as argument separators — so `--spaces in this filename--` gets split into 4 separate arguments. [Command Linux](https://commandlinux.com/how-to/spaces-in-filename/)

Two ways to fix it:

1. **Quotes** → wrap the whole name: `"--spaces in this filename--"`
2. **Backslash** → escape each space: `--spaces\ in\ this\ filename--`


cat "--spaces in this filename--" cmd
             OR
cat ./--spaces\ in\ this\ filename--  cmd

and it revealed me a pwd to the next level

Password String Intentionally Omitted




SOC angle: Malware often uses filenames with spaces or 
unusual characters to hide in plain sight on a compromised system.