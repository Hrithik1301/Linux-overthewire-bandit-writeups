
Connecting to ssh level 11 using the credentials from Prv. level

ssh bandit11@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted

## Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Helpful Reading Material

- [Rot13 on Wikipedia](https://en.wikipedia.org/wiki/ROT13)

How ROT13 Works

The alphabet has 26 letters. The number 13 is exactly half of 26. This means the cipher rotates every letter forward by 13 steps. If it goes past 'Z', it wraps back around to 'A'. 

- `A` becomes `N` (1 + 13 = 14)
- `B` becomes `O` (2 + 13 = 15)
- ...and conversely, `N` wraps back around to become `A`.

Because 13 is exactly half of 26, **the encryption action and the decryption action are identical**. Shifting a letter forward by 13 twice brings you right back to where you started!

bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA

bandit11@bandit:~$ cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
The password is Password String Intentionally Omitted

explanation of the cmd's above


The `tr` command works by expanding character sets inside single quotes and performing a strict, **one-to-one positional mapping** from the first set to the second set

tr - translate cmd syntax

tr 'SET1' 'SET2'

- **`SET1` (The Input Map):** Must contain the full 52-character standard alphabet (`a-zA-Z`).
- **`SET2` (The Output Map):** Must contain the shifted alphabet, split into smaller blocks that wrap around (`n-za-mN-ZA-M`)

How the System Reads It

The computer flattens the shorthand ranges into two perfectly aligned, 52-character rows:

- **Set 1:** `abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ`
- **Set 2:** `nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXYZABCDEFGHIJKLM`

Since `a` aligns with `n`, `b` aligns with `o`, and so on, running this command instantly restores the scrambled text into the cleartext password.


NOTE : if we give az instead of a-z the system only reads two chars a & z instead of a-z which is 26 chars





SOC angle: Simple ciphers like ROT13 are occasionally used 
in CTF malware samples to obscure strings. More importantly, 
the tr command teaches character substitution — the same 
logic behind many encoding and obfuscation techniques 
analysts encounter in the wild.


