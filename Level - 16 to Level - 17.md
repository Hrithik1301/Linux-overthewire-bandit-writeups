

Connecting to ssh level 16 using the credentials from prv level

ssh bandit16@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

**Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.**

## Commands you may need to solve this level

ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

## Helpful Reading Material

- [Port scanner on Wikipedia](https://en.wikipedia.org/wiki/Port_scanner)


bandit16@bandit:~$ nmap -p 31000-32000 localhost
Starting Nmap 7.98 ( https://nmap.org ) at 2026-09-13 17:05 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00038s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.13 seconds
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31046
Connecting to 127.0.0.1
40D7E7F7FF7F0000:error:0A0000F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:423:
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31518
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
^C
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31691
Connecting to 127.0.0.1
40D7E7F7FF7F0000:error:0A0000F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:423:
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31790
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
^C
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31960
Connecting to 127.0.0.1
40D7E7F7FF7F0000:error:0A0000F4:SSL routines:ossl_statem_client_read_transition:unexpected message:../ssl/statem/statem_clnt.c:423:
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31518
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
Password String Intentionally Omitted
Password String Intentionally Omitted
^C
bandit16@bandit:~$ openssl s_client -quiet -connect localhost:31790
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
Password String Intentionally Omitted
Correct!
**Private key contents — intentionally omitted**
bandit16@bandit:~$ logout
Connection to bandit.labs.overthewire.org closed.
hrithik@Hrithik:~$ nano ssh.key17
hrithik@Hrithik:~$ ls
ssh.key  ssh.key17
hrithik@Hrithik:~$ chmod 600 ssh.key17
hrithik@Hrithik:~$ ssh bandit17@bandit.labs.overthewire.org -i ssh.key17 -p 2220
bandit17@bandit:~$ ls 
passwords.new  passwords.old




Explanation of this level step-by-step
1. from the level goal it is clear that we need to scan ports from 31000 to 32000 on localhost, & from prv. level i understood that i need to use "nmap" command
2. so i typed in the command "nmap -h", which returned me with all the flags & parameters along with the syntax
3. so i got the open ports after scanning through ports ranging from 31000-32000 using the command "nmap -p 31000-32000 localhost"
4. from that i got 5 open ports ---> 31046, 31518, 31691, 31790, 31960
5. since it is given in the level goal that the next level's credentials is obtained by sending this level's password to one of this open ports & most importantly it speaks **SSL/TLS** ---> meaning to use openssl command like prv. level
6. so i individually tried to connect to every open port, then port no.'s ---> 31046, 31691, 31960 just returned errors and did not connect
7. the remaining ports ---> 31518 & 31790 actually connected
8. wherein port 31518 was an echo server — it just reflected back whatever I sent, meaning it wasn't the right server
9. and port no. 31790 actually returned me the SSH private key to next level
10. so i copied the SSH private key then logged out then created a new file named ssh.key17 using nano command like one of the previous level's
11. then i changed the file permissions using "chmod 600 ssh.key17" command & set it to only owner read & write
12. now i logged into next level using this ssh private key with the command "ssh bandit17@bandit.labs.overthewire.org -i ssh.key17 -p 2220" 


SOC angle: Port scanning with nmap is a fundamental SOC 
and IR skill. During incident response, analysts scan 
compromised hosts to find unexpected open ports — a 
backdoor or C2 listener often reveals itself as an 
unusual open port. Knowing how to identify which ports 
speak SSL vs plain text is directly applicable to 
analysing suspicious network traffic.

