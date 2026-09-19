
Connecting to ssh level 20 using the credentials from prv level

ssh bandit20@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted 


## Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

**NOTE:** Try connecting to your own network daemon to see if it works as you think

## Commands you may need to solve this level

ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)



bandit20@bandit:~$ ls
suconnect
bandit20@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit21 bandit20 15604 Jun 24 14:58 suconnect
bandit20@bandit:~$ nc -l 12345 &
[1] 202
bandit20@bandit:~$ echo "Password String Intentionally Omitted" | nc -l 1234&
[3] 257
bandit20@bandit:~$ ./suconnect 1234
Read: Password String Intentionally Omitted
Password matches, sending next password
Password String Intentionally Omitted
[3]   Done                       echo "Password String Intentionally Omitted" | nc -l 1234



Explanation of this level step-by-step
1. after logging in, types "ls" to look into what's there ---> suconnect
2. because it is already given in the level goal that it is a setuid binary file, so used "ls -l" to look into the permissions
3. and according to the level goal **NOTE:** Try connecting to your own network daemon to see if it works as you think
4. idk what it was, so i asked ai, what a network daemon was & it explained 
5. A **network daemon** is just a technical, fancy name for a program that runs silently in the background and listens for incoming network connections.
6. and coming to the level goal, honestly i didn't even understand it completely either, so i took the help of ai to tell me the level goal in simple terms and it explained the level goal to me as
7. The Story Behind This Level

You have another SUID file in your home directory (let's call it the **Game Program**). This program has `bandit21`'s powers, but it wants to play a game of "secret handshake" before it gives you the next password.

The Game Program does three things in exact order when you run it:

1. **It knocks on a port:** You have to tell it which port number to connect to (example: `./program 12345`). It will instantly connect to that port on `localhost`.
2. **It listens:** Once connected, it waits for whatever is on the other side of that port to send it a line of text.
3.  **It checks the password:** It takes that text and checks if it matches your current `bandit20` password. If it matches, it hands you the `bandit21` password!

**The Catch** 

Here is your dilemma:

- To get the next password, you need to run the Game Program and make it connect to a port.
- But there isn't a port currently listening on the server waiting to send your password! **You have to create that listening port yourself.**

This means you need to do two things _at the same time_ on the same server:

1. Setup a tool (like `nc`) to **listen** on a custom port and hold your current `bandit20` password ready to send.
2. Run the **Game Program** and tell it to connect to that exact same custom port.


**The Problem: You Only Have One Screen!**

If you use `nc` to listen on a port, it takes over your terminal window. You can't type any more commands until you stop it. But if you stop it, the port closes, and the Game Program can't connect to it!

To solve this, the game suggests using **Unix Job Control** or tools like **`screen` / `tmux`**. These are fancy ways of saying: **"You need a way to run two things at once, or open a second terminal tab."**

and it even gave me a strategy or a hint to work around

Let's look at the easiest way to do this without learning completely new terminal programs like `tmux`. Linux has a feature called **Background Jobs**.

If you type a normal command and put an **ampersand (`&`)** at the very end of it, Linux will run that command in the "background." It stays alive, but it immediately frees up your terminal screen so you can type a second command!


from all the above conversation with ai i understood that i need to create a port in the background where it already has this level's password and runs in the background as well, & when i use the suconnect SUID file to listen to the port i created it listens to the password and verifies it, if the password matches, then i will get a password for the next level. 

so i used nc command to create a custom port & hold my current level password and run in the background as well so i tried " nc -l 12345 & " ---> but i didn't give my pwd so it just listens to nothing, when i tried to "./suconnect 12345" so this time i piped the pwd to the nc command by using "echo "Password String Intentionally Omitted" | nc -l 1234&" & now using the "./suconnect 1234" cmd to listen to the pwd, it verified & gave me the pwd to the next level




SOC angle: Netcat listeners are commonly used by attackers 
to set up reverse shells — the attacker runs nc -l on their 
machine waiting for the victim to connect back. Seeing 
outbound nc connections in SIEM logs, especially to unusual 
ports, is a high-priority alert. Background jobs (&) are 
also used by attackers to keep malicious processes running 
silently after they disconnect.





