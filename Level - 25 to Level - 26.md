

Connecting to ssh level 25 using the credentials from Prv level

ssh bandit25@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


## Level Goal

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not **/bin/bash**, but something else. Find out what it is, how it works and how to break out of it.

> NOTE: if you’re a Windows user and typically use Powershell to `ssh` into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

## Commands you may need to solve this level

ssh, cat, more, vi, ls, id, pwd


bandit25@bandit:~$ ls
bandit26.sshkey
bandit25@bandit:~$ cat bandit26.sshkey
**Private key contents — intentionally omitted**

bandit25@bandit:~$ logout
Connection to bandit.labs.overthewire.org closed.
hrithik@Hrithik:~$ nano sshkey.bandit26
hrithik@Hrithik:~$ ls
ssh.key  ssh.key17 sshkey.bandit26
hrithik@Hrithik:~$ chmod 600 sshkey.bandit26
hrithik@Hrithik:~$ ssh bandit26@bandit.labs.overthewire.org -i sshkey.bandit26 -p 2220



Explanation of this level step-by-step
1. logged in ---> types ls ---> found bandit26.sshkey
2. cat bandit26.sshkey ---> ssh private key
3. copied the ssh key ---> logged out
4. used nano sshkey.bandit26 ---> to create a file & pasted the above copied ssh key ---> ctrl+o ---> enter ---> ctrl+x
5. then used chmod 600 sshkey.bandit26 ---> to change file permissions
6. then used ssh bandit26@bandit.labs.overthewire.org -i sshkey.bandit26 -p 2220 to login to next level ---> but it logged me out immediately


NOTE: The solution to actually breaking out of this 
restricted shell is documented in Level 26→27, as 
both levels are solved together in sequence.



SOC angle: Restricted shells are used by organisations 
to limit what a user can do after logging in — a 
security control. Attackers who gain initial access 
to a restricted shell look for exactly this kind of 
escape technique to break out to a full shell. 
Understanding how restricted shells work and how 
they can be escaped is directly relevant to SOC 
incident response on compromised Linux systems.


