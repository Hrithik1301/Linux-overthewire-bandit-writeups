
Connecting to ssh level 17 using the credentials from prv level

ssh bandit17@bandit.labs.overthewire.org -i ssh.key17 -p 2220


## Level Goal

There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

## Commands you may need to solve this level

cat, grep, ls, diff




bandit17@bandit:~$ ls
passwords.new  passwords.old
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
 < Password String Intentionally Omitted
---    > Password String Intentionally Omitted


The Breakdown

1. **`42c42` (The Location):**  
    This tells you the exact line number where the difference was found. It reads: _"Line **42** in the first file needs to be **C**hanged to match line **42** in the second file."_
2. **`< Password String Intentionally Omitted` (The Old File):**  
    The less-than sign (`<`) points to the **left** (the first file you listed, which is `passwords.old`). This is the old, outdated password from the previous level.
3. **`---` (The Divider):**  
    This simply separates the old file's contents from the new file's contents.
4. **`> Password String Intentionally Omitted` (The New File):**  
    The greater-than sign (`>`) points to the **right** (the second file you listed, which is `passwords.new`). This is the brand-new line that replaced the old one


The `diff` command analyzes two text files line-by-line and spits out an exact roadmap of their differences. It tells you what needs to be added, deleted, or changed to make the first file match the second file. It is the premier tool when you want to compare **two distinct files** against each other.

Syntax ---> diff [options] file1 file2



Explanation of this level step-by-step

1. logged into this level from the ssh private key from prv. level
2. then used ls to view the files in this level
3. then i got 2 files as mentioned in the level goal
4. looked at the commands you may need to solve this level section from the level goal and used ai to get the syntax and usage of the commands there
5. used diff command and got the password for next level



SOC angle: The diff command is used in security to 
compare configuration files before and after a suspected 
compromise — detecting unauthorized changes to critical 
files like /etc/passwd, crontabs, or firewall rules. 
File integrity monitoring (FIM) tools like Tripwire 
work on the same principle as diff.



