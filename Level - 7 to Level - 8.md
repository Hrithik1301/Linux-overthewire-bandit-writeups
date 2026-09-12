
Connecting to ssh level 7 using the credentials from Prv. level

ssh bandit7@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Commands you may need to solve this level

[man](https://manpages.ubuntu.com/manpages/noble/man1/man.1.html), grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd


bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep millionth data.txt
millionth      Password String Intentionally Omitted


NOTE : 
`grep` searches for a pattern inside files.

```
grep "hello" file.txt
```

Prints every line in `file.txt` containing the word "hello".

**Common flags:**

- `-i` → case-insensitive
- `-r` → search recursively through folders
- `-n` → show line numbers
- `-v` → show lines that DON'T match


| Command   | What it does                                           |
| --------- | ------------------------------------------------------ |
| `grep`    | Searches for a word/pattern inside a file              |
| `sort`    | Sorts lines alphabetically or numerically              |
| `uniq`    | Removes duplicate lines                                |
| `strings` | Extracts readable text from binary files               |
| `base64`  | Encodes/decodes base64 data                            |
| `tr`      | Translates or replaces characters                      |
| `tar`     | Archives/extracts multiple files                       |
| `gzip`    | Compresses/decompresses files                          |
| `bzip2`   | Compresses/decompresses files (better ratio than gzip) |
| `xxd`     | Shows file contents in hex format                      |





SOC angle: grep is used daily in SOC to search log files 
for IOCs — suspicious IPs, domain names, usernames, 
or error codes. Knowing grep flags like -i, -r, and -n 
directly speeds up log analysis.


