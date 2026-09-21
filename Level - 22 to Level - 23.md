

Connecting to ssh level 22 using the credentials from Prv level

ssh bandit22@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)



bandit22@bandit:~$ cd /etc/cron.d/
bandit22@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@bandit:/tmp$ echo "I am user bandit23" | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cd /tmp
bandit22@bandit:/tmp$ cat 8ca319486bfbbc3663ea0fbe81326349
Password String Intentionally Omitted


Explanation of this level step-by-step
1. after logging in, according to the level goal i looked in **/etc/cron.d/**, by using cd & then ls cmd's
2. then i looked in to the cronjob_bandit23 using cat cmd, bcoz it seemed relevant to the next level
3. it gave me the file path for shell script i.e., /usr/bin/cronjob_bandit23.sh
4. so again i used cat cmd to reveal the script at /usr/bin/cronjob_bandit23.sh
5. i understood the code a bit, and idk the md5 algo, so i used ai to understand the code line by line and it gave me
6. Line-by-Line Breakdown

7. `#!/bin/bash`

- **What it means:** This is called a **shebang**. It tells the operating system: _"Hey, this is a script file. Please use the Bash terminal interpreter to run the commands inside me."_

2. `myname=$(whoami)`

- **What it means:** It runs the `whoami` command (which prints the name of whoever is running the script) and saves that result inside a shortcut variable called `$myname`.
- **Why this matters:** Since the automated system runs this script as **`bandit23`**, the variable `$myname` becomes equal to the text string `"bandit23"`.

3. `mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)`

- **What it means:** This runs the exact text-scrambling pipeline we just talked about.
- **The Result:** It takes `"I am user bandit23"`, passes it through the math hashing- engine, cuts off the extra spaces, and saves that unique 32-character string (`8ca319486bfbbc3663ea0fbe81326349`) into a new variable called `$mytarget`.

4. `echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"`

- **What it means:** This just prints a helpful status message out loud, mostly for logging purposes. If you could see it, it would read: _"Copying passwordfile /etc/bandit_pass/bandit23 to /tmp/8ca319486bfbbc3663ea0fbe81326349"_.

5. `cat /etc/bandit_pass/$myname > /tmp/$mytarget`

- **What it means:** This is the core action of the script.
    - It reads the secret password file belonging to `bandit23` (`cat /etc/bandit_pass/bandit23`).
    - It uses the **`>`** arrow to copy and dump that text directly into a brand new file inside the temporary folder using the hashed name we calculated (`/tmp/8ca319486bfbbc3663ea0fbe81326349`).


it directly gave me the file name, but i used "echo "I am user bandit23" | md5sum | cut -d ' ' -f 1" cmd to get the file name, as i understood a few lines of code even before i used ai. next i cd into /tmp and used "cat 8ca319486bfbbc3663ea0fbe81326349" to get the pwd for bandit23, a small note here is i could've used "cat /tmp/8ca319486bfbbc3663ea0fbe81326349", directly & still would've got the pwd like prv level. 



SOC angle: MD5 hashing appears constantly in SOC work — 
file hashes are used as IOCs to identify known malware. 
If a suspicious file's MD5 hash matches a known bad hash 
in VirusTotal or threat intel feeds, it confirms malicious 
activity. Understanding how md5sum works and how to 
generate hashes from the command line is a direct 
SOC analyst skill.