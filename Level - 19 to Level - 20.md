
Connecting to ssh level 19 using the credentials from Prv level

ssh bandit19@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted 


## Level Goal

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Helpful Reading Material

- [setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)



bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ls-l
ls-l: command not found
bandit19@bandit:~$ ls -l
total 16
-rwsr-x--- 1 bandit20 bandit19 14880 Jun 24 14:58 bandit20-do
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do whoami
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
Password String Intentionally Omitted



Explanation of this level step-by-step
1. logged in to this level using the credentials from prv level, and typed "ls" cmd
2. it showed one single file "bandit20-do"
3. and by using "ls -l" it gave me the permissions list for that file as "-rwsr-x--- 1 bandit20 bandit19 14880 Jun 24 14:58 bandit20-do"
4. in the level goal it is given to know about "setUID" ---> so i asked ai about it & it gave me a anology about it

Imagine you want to look at a highly confidential medical file in a hospital, but you are just a regular visitor. The security guard blocks you because you don't have the clearance.

However, the chief doctor has a special stamp. If the doctor stamps a specific request form, the security guard will look at the stamp, temporarily treat _you_ as if you have the doctor's authority, and hand you the file **just for that one task**. The moment you step away, you go back to being a normal visitor.

In Linux, **SUID** (which stands for **Set User ID**) is that special stamp

How it works in Linux:

Normally, when you run a program, that program operates with **your** exact permissions. If you aren't allowed to read a file, any program you run can't read it either.

But if a program has the **SUID stamp** turned on:

1. The file owner is usually a powerful account (like `root` or `bandit20`).
2. When you (a regular user) execute that program, the system temporarily **boosts your authority**
3. For the entire time that specific program is running, it runs with the power of the **file's owner**, not you.
4. As soon as the program finishes, your temporary superpowers vanish

the explanation for the output printed when "ls -l"  command is used is as below

The Permissions: `-rwsr-x---`

This is a 10-character string that shows who is allowed to do what. We split it into four parts:

- **`-` (First character):** This simply means it is a regular **file** (if it were a directory, it would be a `d`).
- **`rws` (Next 3 characters - User/Owner permissions):** This belongs to the owner (`bandit20`). They can **R**ead, **W**rite, and the **`s`** is the **SUID stamp** we just talked about. It means when _anyone_ runs this file, it temporarily inherits `bandit20`'s powers.
- **`r-x` (Next 3 characters - Group permissions):** This belongs to the group (`bandit19`). Anyone in the `bandit19` group can **R**ead and e**X**ecute (run) this file. (Since you are logged in as `bandit19`, this means _you_ are allowed to run it!).
- **`---` (Last 3 characters - Everyone else):** Anyone else on the server who isn't the owner or in the group has zero permissions. They can't read it, write to it, or run it.

The Owner: `bandit20`

This tells us that the file belongs to the user account **`bandit20`**. This is critical because it means when the SUID stamp triggers, the file will run with `bandit20`'s privileges.

The Group: `bandit19`

This tells us the file is associated with the **`bandit19`** group.

The File Size: `14880`

The file size is exactly **14,880 bytes**.

then i used the command "./bandit20-do cat /etc/bandit_pass/bandit20" to get the password for the next level



SOC angle: SUID binaries are a critical privilege escalation 
vector. During a Linux compromise, attackers look for SUID 
binaries owned by root to escalate from a low-privilege 
user to root. SOC analysts and IR teams run "find / -perm 
-4000" to list all SUID binaries on a suspicious system — 
any unexpected SUID binary is a major red flag.




