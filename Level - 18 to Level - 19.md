

Connecting to ssh level 18 using the credentials from prv level

ssh bandit18@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
Password String Intentionally Omitted


## Level Goal

The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

## Commands you may need to solve this level

ssh, ls, cat



Byebye !
 ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
 bandit18@bandit.labs.overthewire.org's password: Password String Intentionally Omitted
Password String Intentionally Omitted



Explanation of this level step-by-step
1. tried to login using the credentials from prv level.
2. but as stated in the prv level 's  level goal it printed a "byebye!" msg & closed my connection 
3. to understand what is actually happening i looked into the level goal & it said something about .bashrc (idk what it is)
4. so i used ai to understand what it is & it explained the following things to me in detail 
5. What is `.bashrc`?

Every time you log into a Linux server using SSH, the server spawns a shell (usually `bash`) for you to type commands. Before it hands control over to you, `bash` automatically looks for a hidden startup script in your home directory named **`.bashrc`**.

System administrators and users use `.bashrc` to set up their environment—like creating shortcuts, changing terminal colors, or setting paths. It runs automatically, line by line, the exact millisecond you connect.

The Sabotage

The level goal tells you that someone modified `bandit18`'s `.bashrc` file to include a command like `exit` or `logout`.

So here is the sequence of what is happening:

1. You SSH in with the correct password.
2. The server says "Welcome!" and launches your `bash` shell
3. - Your shell reads `.bashrc` and executes the nasty `exit` command inside it.
4. The terminal prints `"byebye"` and slams the door shut before you can type a single thing.

and it gave me a hint to work around

To beat this trap, you need to understand that the `ssh` command doesn't _just_ have to open an interactive terminal. It is actually designed to let you **send a specific command over the wire**, execute it immediately on the server, and send the results back to your screen without ever opening the regular interactive login shell.

If you tell SSH to execute a specific command directly at the moment of connection, it completely bypasses the normal interactive shell startup routines (and avoids triggering the `.bashrc` trap!).

For example, if you run a command like `ssh bandit18@host "whoami"`, it will log in, run `whoami`, print the username on your screen, and close the connection cleanly.

so looking at the commands to solve this level i appended the cat command to my login command like "ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme", it in turn asked for a password so i entered "Password String Intentionally Omitted", (obtained from prv level), then it gave me "Password String Intentionally Omitted" (password for the next level), instead of printing a byebye! msg and closed the connection




SOC angle: Attackers commonly modify .bashrc, .bash_profile, 
or .profile on compromised Linux systems to maintain 
persistence — running malicious scripts every time the 
user logs in. During IR, checking startup scripts is a 
standard step. The SSH remote command execution technique 
used here also mirrors how attackers run commands on 
compromised servers without an interactive shell.