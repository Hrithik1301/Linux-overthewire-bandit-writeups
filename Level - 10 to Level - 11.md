
Connecting to ssh level 10 using the credentials from Prv. level

ssh bandit10@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Helpful Reading Material

- [Base64 on Wikipedia](https://en.wikipedia.org/wiki/Base64)

after entering this level with "ls" cmd it gave data.txt file and applying cat to data.txt file it gave a random base64 encoded string "VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg=="

**Base64 is a translation system.** It takes raw data and translates it into a safe, universal alphabet consisting of only 64 characters: 

- Uppercase letters (`A–Z`)
- Lowercase letters (`a–z`)
- Numbers (`0–9`)
- Two symbols (usually `+` and `/`)
- An equals sign (`=`) used at the very end as a spacer (padding)
- 
Look closely at the string your `cat` command printed:  
`VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg==`

- It uses a mix of uppercase letters, lowercase letters, and numbers.
- It finishes with **`==`**. This padding is the ultimate signature of a Base64 string! It tells the decoder, _"The message ends here_

syntax :

 base64 [options] [file]  

OPTIONS
       -d, --decode
              decode data

       -i, --ignore-garbage
              when decoding, ignore non-alphabetic characters

       -w, --wrap <COLS>
              wrap encoded lines after COLS character (default 76, 0 to disable wrapping)



bandit10@bandit:~$ base64 -d data.txt
The password is Password String Intentionally Omitted






SOC angle: Base64 is heavily used by attackers to obfuscate 
payloads in phishing emails, PowerShell commands, and C2 
traffic. Recognising and decoding base64 is a daily SOC skill.