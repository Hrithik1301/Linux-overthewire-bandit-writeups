
first i installed the wsl (windows subsystem for linux), then i created a username & pwd

for remotely connecting to the bandit website @ port no. 2220 i used the following command in the ubuntu wsl 

Syntax :

ssh username@host -p port no.

command :

ssh bandit0@bandit.labs.overthewire.org -p 2220

after entering the command it asked for a pwd so " bandit0 "

as per the instructions given in the overthewire-bandit website

NOTE : `-p` specifies the **port number**.

SSH connects to port **22 by default**. But Bandit uses port **2220**, so `-p 2220` tells SSH to connect there instead of the default.

Without `-p 2220` → connection fails.


NOTE 2 : the username&pwd for the website along with the host name and port number are given in the website.


SOC angle: Unusual SSH logins are one of the most common alerts 
in a SOC. Always check source IP, time, and whether the user 
normally logs in from that location.

