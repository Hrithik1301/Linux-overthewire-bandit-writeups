
Connecting to ssh level 3 using the credentials from Prv. level

ssh bandit3@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in a hidden file in the **inhere** directory.

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html)

as ususal used "ls" cmd

displayed a folder named inhere

used "cd inhere" cmd to navigate to the inhere directory

used "ls" again

shows nothing

so i used my intuition to solve this level and typed "du" (data usage) cmd but since i'm already inside the "inhere" directory the terminal returned this error "du: cannot access 'inhere': No such file or directory", then i quickly pivoted back to the home directory using "cd .." cmd now i used "du -h inhere" cmd then the terminal gave me "8.0K    inhere", meaning that the inhere directory has 8.0K bytes of data(i.e, 8KB), so then again i navigated back into the directory using "cd inhere" cmd, now i used the "find" cmd and the terminal returned me with " ./...Hiding-From-You ", meaning that the directory inhere has a file named "...Hiding-From-You", so i utilized the knowledge gained in previous level and entered the following cmd 

cat "...Hiding-From-You" 
          OR
cat ...Hiding-From-You
 and it gave me the pwd to the next level 
Password String Intentionally Omitted

NOTE : Hidden files in Linux start with a `.` dot — that's why `ls` showed nothing. `ls -a` reveals hidden files. Remember that for future levels.

Upon using ls -a cmd given by claude the terminal returned the following

.  ..  ...Hiding-From-You

. = current directory (wherever you are right now)
.. = parent directory (one level up)
These mean the same thing in EVERY Linux directory, not just inhere.

"...Hiding-From-You" is the actual hidden filename

NOTE 2 : 
- `ls -a` → shows **all** files including hidden ones (dots files)
- `du -h` → shows size in **human-readable** format (KB, MB, GB instead of raw bytes)




SOC angle: Attackers commonly hide malicious scripts and 
persistence files as dot files (e.g. .bashrc, .profile) 
on compromised Linux systems. ls -a is a standard IR step.