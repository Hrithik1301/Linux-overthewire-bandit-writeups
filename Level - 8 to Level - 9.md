
Connecting to ssh level 8 using the credentials from Prv. level

ssh bandit8@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd


Helpful Reading Material

- [Piping and Redirection](https://ryanstutorials.net/linuxtutorial/piping.php)

```
uniq [options] filename
```

Common flags:

- `-c` → count occurrences
- `-d` → show only duplicates
- `-u` → show only unique lines


```
sort [options] filename
```

Common flags:

- `-r` → reverse order
- `-n` → numeric sort
- `-u` → sort + remove duplicates


```
sort data.txt | uniq -u
```

`|` passes output of `sort` as input to `uniq`.


bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ sort data.txt | uniq -u
Password String Intentionally Omitted





SOC angle: Identifying unique or duplicate entries in logs 
is essential for detecting anomalies — one login from 
an unusual country in 10,000 lines shows up only when 
you can filter for unique occurrences.