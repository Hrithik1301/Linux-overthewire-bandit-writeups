

Connecting to ssh level 14 using the credentials from Prv level


ssh bandit14@bandit.labs.overthewire.org -i ssh.key -p 2220
No password as we used SSH key as login method


Level Goal 

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap 

Helpful Reading Material

How the Internet works in 5 minutes (YouTube) (Not completely accurate, but good enough for beginners) IP Addresses IP Address on Wikipedia Localhost on Wikipedia Ports Port (computer networking) on Wikipedia





bandit14@bandit:~$ /etc/bandit_pass/bandit14
-bash: /etc/bandit_pass/bandit14: Permission denied
bandit14@bandit:~$ cd /etc/bandit_pass/bandit14
-bash: cd: /etc/bandit_pass/bandit14: Not a directory
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
Password String Intentionally Omitted
bandit14@bandit:~$ nc localhost 30000
Password String Intentionally Omitted
Correct!
Password String Intentionally Omitted

^C
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Password String Intentionally Omitted
Correct!
Password String Intentionally Omitted

Connection closed by foreign host.



Explanation of this level step-by-step

1. i logged into this level using a ssh private key instead of a password, but according to the previous level's level goal the password for this level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**, so i took a detailed look at this level's useful commands & reading material 
2. then i directly typed the path "/etc/bandit_pass/bandit14" it gave me a error permission denied
3. then i thought i should cd to this path & tried that too but again error that it was not a directory
4. then i thought may be it is a file name so i tried the cat command then i got the password "Password String Intentionally Omitted" for this level, now the level goal was to give this password as a input, after connecting to a localhost at port no 30000
5. so i used nc command ---> syntax : nc host_name port_no. to connect to port 30000 on localhost
6. then copied the password and pasted it here then it generated a message saying "correct and Password String Intentionally Omitted" which is the password to the next level
7. and i also used telnet to see how it works it gave me the same password as well


Some important notes on commands for this level


- **`nc` (Netcat):** The rawest, simplest tool. It opens a plain, unencrypted pipe to a port and sends raw text. Perfect for this level because port 30000 was expecting plain text.
- **`telnet`:** An older tool designed to log into remote computers. Before `nc` became popular, engineers used `telnet localhost 30000` to test ports because it behaves almost exactly like Netcat when connecting to raw text ports.
- **`openssl s_client`:** This is like Netcat, but with a massive upgrade: **encryption**. If port 30000 was wrapped in an SSL/TLS security blanket (like a website using `https://`), plain Netcat would fail, but `openssl` would successfully talk to it.
- **`nmap`:** This is a scanner. It doesn't send passwords; it maps out the building. If the game didn't tell you the port was 30000, you would use `nmap` to scan the server and find which ports were open and listening.


SOC angle: nc (Netcat) is called the "Swiss Army knife" of 
networking and is used daily in SOC and incident response — 
to test if a port is open, to transfer files, or to set up 
quick listeners. Attackers also use it to create reverse 
shells, so nc activity on unusual ports in your SIEM logs 
is always worth investigating.


