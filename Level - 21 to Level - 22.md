
Connecting to ssh level 21 using the credentials from prv level

ssh bandit21@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)



bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Password String Intentionally Omitted



Explanation of this level step-by-step
1. after logging in, according to the level goal, i must look in **/etc/cron.d/** for the configuration, so used cd  
2. and idk what cron is, so i used man cron to know about it ---> cron - daemon to execute scheduled commands 
3. since the ls showed the files & from there i only considered cronjob_bandit22 relevant, bcoz it is the next level
4. so i looked into the cronjob_bandit22 file with cat cronjob_bandit22 cmd & terminal gave me this output (which i didn't understand) ---> @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

**Breaking Down the Configuration Lines**
- **The Stars (`* * * * *`):** The five asterisks represent time (Minutes, Hours, Day of Month, Month, Day of Week). An asterisk means "every." So `* * * * *` means **"run this command every single minute of every single day."**
- **The User (`bandit22`):** This tells the system _who_ is running the script. The script runs with the authority and permissions of **`bandit22`**!
- **The Script (`/usr/bin/cronjob_bandit22.sh`):** This is the exact path to the shell script (a file full of terminal commands) that gets executed every minute.
- **The Silencer (`&> /dev/null`):** This takes any errors or standard text the script might print out and throws it into a digital trash can called `/dev/null`. It ensures the script runs completely invisibly.

it gave me the path to shell script, so i used cat cmd to look into the .sh file ---> "cat /usr/bin/cronjob_bandit22.sh", which in turn gave "#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv"

That script is exactly what is running invisibly every single minute. Let's look at exactly what it just did :

1. **`chmod 644 /tmp/t7O6lds...`**: It changes the permissions of a temporary file to make sure it is readable by everyone on the system (including you!).
2. **`cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds...`**: It grabs the secret password for `bandit22` and uses the **`>`** arrow to copy/paste it directly into that long temporary file inside the `/tmp` folder.

so i understood that the pwd for bandit22 is at /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv so i used cat cmd to extract the pwd for bandit22



SOC angle: Cron jobs are one of the most common persistence 
mechanisms used by attackers on Linux systems. After gaining 
access, attackers add malicious cron jobs to /etc/cron.d/ 
or the user's crontab to run their backdoor every minute 
or on reboot. During IR on a compromised Linux host, 
checking /etc/cron.d/, /etc/crontab, and each user's 
crontab is a standard step. The &> /dev/null trick is 
also used by attackers to hide their cron job output 
from system logs.



