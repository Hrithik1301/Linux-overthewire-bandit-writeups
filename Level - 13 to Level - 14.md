

Connecting to ssh level 13 using the credentials from Prv. level

ssh bandit13@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


## Level Goal

The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.  
If you need help with this level: a hint file can be found in the home directory.  
Make sure to read the error messages as they are informative.

## Commands you may need to solve this level

ssh, scp, umask, chmod, cat, nc, install

## Helpful Reading Material

- [SSH/OpenSSH/Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)
- [Transferring Files via SCP](https://help.ubuntu.com/community/SSH/TransferFiles)





After logging in using the credentials from the previous level

bandit13@bandit:~$ ls
HINT  sshkey.private
bandit13@bandit:~$ cat HINT
If you have trouble with this level, note the following:

1) As for all other levels, this level has a website with information:
   https://overthewire.org/wargames/bandit/bandit14.html
2) No, the level is not broken. To verify, see:
   https://status.overthewire.org/
3) The current version of OverTheWire prevents logging in from one
   level to another via localhost. Log out, and see 1)
4) If you get errors, read the error message on your screen.
   We mean it!
bandit13@bandit:~$ cat sshkey.private
**Private key contents — intentionally omitted**
bandit13@bandit:~$ nano ssh.key
Unable to create directory /home/bandit13/.local/share/nano/: No such file or directory
It is required for saving/loading search history or cursor positions.

bandit13@bandit:~$ logout
hrithik@Hrithik:~$ pwd (pwd ---> present working directory)
/home/hrithik
hrithik@Hrithik:~$ nano ssh.key (after this i pasted the copied sshkey.private text ---> ctrl+o ---> enter ---> ctrl+x)
hrithik@Hrithik:~$ ls
ssh.key
hrithik@Hrithik:~$ ssh bandit14@bandit.labs.overthewire.org -i ssh.key -p 2220
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for 'ssh.key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "ssh.key": bad permissions

hrithik@Hrithik:~$ chmod 600 ssh.key
hrithik@Hrithik:~$ ssh bandit14@bandit.labs.overthewire.org -i ssh.key -p 2220
bandit14@bandit:~$ ---> meaning logged in to level14, as the username shows bandit14


Explanation of this level step-by-step

1. After logging in using the credentials from the previous level, i used "ls" command to view the list of files available
2. then cat HINT (showed the rules like checking if the level is broken or not, error msg if any, & the main hint here is that **level to level localhost login is not allowed**)
3. then cat sshkey.private (it showed some encrypted text)
4. then i looked at the level goal as it says i don't get a password to next level instead it gives me a SSH private key to login to next level (idk what it was at the beginning so i used ai to give me a brief description of the helpful reading materials & commands of this level given in the level goal)
5. and it gave me the notes about SSH keys ---> **SSH keys** act like an automated digital ID card. Instead of typing a traditional password, your computer presents a unique cryptographic file (the **private key**) to the server to prove who you are. 
6. **The Catch:** Because private keys grant immediate access without typing a password, SSH is incredibly strict about security. If a private key file is readable by just anyone on a system, SSH will completely refuse to use it. It must be locked down so only the owner can read it.
7. then to actually login to level 14 without a password i needed to identify the flag i need to use so ---> i typed man ssh for the flags available for ssh command and with the description i understood it is "-i"
8. but then i also need to pass the text file as a argument, then i tried to create a file using nano file_name (ssh.key here) & copy pasted the sshkey.private text but i was unable to save it.
9. then i logged out of bandit13, and used the command "pwd" to see my present working directory & then used nano to create the same file ssh.key & copy pasted the encrypted private key text
10. then tried to login using "ssh bandit14@bandit.labs.overthewire.org -i ssh.key -p 2220" command but again error "ssh keys are too open, bad permissions"
11. then i remembered that only owner should have read+write permissions so changed the ssh.key file permissions using "chmod 600 ssh.key" command
12.  then again tried to login using "ssh bandit14@bandit.labs.overthewire.org -i ssh.key -p 2220"
13. now, i'm logged in as bandit14 user so succeeful login to next level using ssh key

NOTE : about file permissions

- **First digit:** What the Owner (you) can do.
- **Second digit:** What the Group can do.
- **Third digit:** What Everyone Else can do.

For numbers: `4` = Read, `2` = Write, `1` = Execute.  
If you want **Read (4) + Write (2)** for yourself, that equals **6**. If you want absolutely no access (0) for everyone else, the digits are **0** and **0**.


SOC angle: SSH private keys are high-value targets for attackers. 
A compromised private key allows passwordless access to any server 
it is authorised on. In SOC investigations, finding an unexpected 
private key on a system is a critical IOC — it may indicate an 
attacker has planted a backdoor for persistent access. chmod 600 
is also a standard hardening check — overly permissive key files 
(0644) are flagged in security audits.

