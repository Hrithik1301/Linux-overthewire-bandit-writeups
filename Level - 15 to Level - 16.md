
Connecting to ssh level 15 using the credentials from prv level

ssh bandit15@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted


## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL/TLS encryption.

**Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.**

## Commands you may need to solve this level

ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

## Helpful Reading Material

- [Secure Socket Layer/Transport Layer Security on Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security)
- [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/testing-with-openssl/index.html)


bandit15@bandit:~$ man openssl
bandit15@bandit:~$ openssl s_client -connect localhost:30001
Connecting to 127.0.0.1
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
---
Certificate chain
 0 s:CN=SnakeOil
   i:CN=SnakeOil
   a:PKEY: RSA, 4096 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN=SnakeOil
issuer=CN=SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: rsa_pss_rsae_sha256
Negotiated TLS1.3 group: X25519MLKEM768
---
SSL handshake has read 3191 bytes and written 1613 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 4096 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 5709F64252E9215F1D47A2506991536D6403C05D9F9620D0F52C77ED475D0688
    Session-ID-ctx:
    Resumption PSK: 7D3E03FB26560CF7728AA69D6E214F3F10A726B2413AB536FF5DC21EBD1C34C51EBF9DEE8BAF6419BABC6579EA96F601
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - d3 36 31 7d b1 9c 35 85-7c 6b 2c a8 28 1c e7 d8   .61}..5.|k,.(...
    0010 - ec 91 dc a3 b8 4f 6b b5-fa c1 a1 0d d6 6d 01 54   .....Ok......m.T
    0020 - 05 dc 4d c9 16 db 74 76-e1 cc 1f a0 a1 83 f2 51   ..M...tv.......Q
    0030 - d2 40 52 bc d0 9d 46 cc-15 91 47 2c 7d 04 4e 42   .@R...F...G,}.NB
    0040 - d7 cf 7f 20 cd be 4d 30-c3 c0 59 4e 7c 9e 2e 6f   ... ..M0..YN|..o
    0050 - b2 da 57 f1 37 65 9c 7b-24 a0 d7 ed 58 03 77 91   ..W.7e.{$...X.w.
    0060 - e8 40 54 29 0a 2f 29 54-7d 36 f4 c6 42 ca 4d 6c   .@T)./)T}6..B.Ml
    0070 - 56 b9 5c a3 77 01 1e 30-a2 87 ca 64 68 49 cc 47   V.\.w..0...dhI.G
    0080 - 3e 32 d1 7a c1 62 4f 2f-55 a6 10 8e dc 67 73 19   >2.z.bO/U....gs.
    0090 - d4 3f 90 b9 72 f5 8a 30-25 f5 68 cc 67 02 e0 0d   .?..r..0%.h.g...
    00a0 - 8c 89 e1 a4 1d 35 19 a2-94 b7 76 bb b0 f1 d8 e2   .....5....v.....
    00b0 - c6 f8 4f 79 09 56 57 15-aa 78 49 51 df 75 da 09   ..Oy.VW..xIQ.u..
    00c0 - 4d 48 2d bf 7e 45 96 2b-e4 75 38 b5 08 c1 56 28   MH-.~E.+.u8...V(
    00d0 - d8 79 20 49 cf 03 b8 73-b7 8f 09 5d 9d e4 94 fd   .y I...s...]....

    Start Time: 1789313456
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 64694CA6DD162FEE20B65D52E277D6DB9CD40C9C00BBB1DA6BAE0D73B480A447
    Session-ID-ctx:
    Resumption PSK: 02E8DE79E0C5B902DF10C8385D4EC16A5C991AF081A4EE348DF882958109458F73433FDA621593BEC8DDE481CB8A3774
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - d3 36 31 7d b1 9c 35 85-7c 6b 2c a8 28 1c e7 d8   .61}..5.|k,.(...
    0010 - 86 e7 93 72 35 14 08 bd-2d 7d 19 d6 03 3c f6 f4   ...r5...-}...<..
    0020 - 20 a2 8a e3 b5 2e 05 6f-30 0c ba 94 9a 8c 4a 59    ......o0.....JY
    0030 - 00 c6 ca 8d 54 80 48 2b-91 b7 82 12 16 40 eb 0f   ....T.H+.....@..
    0040 - d2 d2 76 6b e3 91 b4 cc-1b 4e de 0c 8c 0b 74 0f   ..vk.....N....t.
    0050 - bd 9b 60 3d 9b a5 30 1e-91 e1 47 8b f7 8d 9b 15   ..`=..0...G.....
    0060 - 75 41 aa 95 2b 82 91 5c-af 47 cb eb 99 13 4d ba   uA..+..\.G....M.
    0070 - 52 1b 23 c4 c4 9d 4e 35-a9 0a 44 68 ac e7 da ac   R.#...N5..Dh....
    0080 - 2e b6 a5 8f bc 79 f5 b6-70 c1 85 59 1e f8 88 90   .....y..p..Y....
    0090 - b1 07 c4 b4 e7 47 c9 96-cd 29 88 bc 71 9e ec ae   .....G...)..q...
    00a0 - fa 78 7c 51 a9 e6 96 54-75 e9 12 b2 dd 7a c0 91   .x|Q...Tu....z..
    00b0 - 8d 4f 06 4a c7 ac ec 63-ae f0 81 ce 1d ee 5b dc   .O.J...c......[.
    00c0 - b6 5d 13 3e 4e 42 17 1a-07 75 6d 47 95 28 c0 92   .].>NB...umG.(..
    00d0 - f2 1f a8 e3 48 1b 6d a0-14 eb bc d4 01 ae a9 d6   ....H.m.........

    Start Time: 1789313456
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Password String Intentionally Omitted
Correct!
Password String Intentionally Omitted

closed



OR


bandit15@bandit:~$ openssl s_client -quiet -connect localhost:30001
Connecting to 127.0.0.1
Can't use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
Password String Intentionally Omitted
Correct!
Password String Intentionally Omitted



Explanation of this level step-by-step
1. logged in to this level using the credentials from the prv. level
2. as stated in the level goal, i must use ssl/tls encryption to connect to localhost 30001 port no.
3. so i looked into man openssl
4. then i used ai to get the syntax for openssl along with its flags & parameters
5. then i used the command "openssl s_client -connect localhost:30001" to securely connect to localhost 30001 port no. 
6. then it printed the SSL/TLS certificate details and handshake information.
7. and then i pasted the current level's password 
8. and got the message "correct!" and the password for next level
9. to avoid the text i modified the command to "openssl s_client -quiet -connect localhost:30001"


Some important notes on commands for this level

openssl basic syntax ---> openssl s_client -connect host:port flags

- _What it does:_ Specifies the destination server and port number.
- _Note:_ The host and port **must** be separated by a colon (`:`), not a space

- **`-quiet`**
    - _What it does:_ Suppresses the massive wall of cryptographic handshake text, session parameters, and certificate details. It keeps your terminal clean so you only see the actual server data.


The **`s_client`** part of the command stands for **"SSL/TLS Client"**.

In networking, communication is a two-way street between a **client** (the program requesting data) and a **server** (the program listening for requests and serving data).

When you use the `openssl` tool, it needs to know what role you want it to play. By typing **`s_client`**, you are telling OpenSSL:  
_"Act like a secure client. Go out onto the network, knock on a server's door, handle the encrypted security handshake, and open a portal for me to talk to it."_



SOC angle: SSL/TLS inspection is a core SOC skill. 
Self-signed certificates (like "CN=SnakeOil" here) are 
a common red flag in security alerts — legitimate services 
use CA-signed certificates. Seeing a self-signed cert 
in traffic analysis is an IOC worth investigating.






