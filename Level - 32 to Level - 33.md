
Connecting to ssh level 32 using the credentials from Prv level

ssh bandit32@bandit.labs.overthewire.org -p 2220
Password String Intentionally Omitted (pwd)


## Level Goal

After all this `git` stuff, it’s time for another escape. Good luck!

## Commands you may need to solve this level

sh, man



WELCOME TO THE UPPERCASE SHELL
>> $0
$ cat /etc/bandit_pass/bandit33
Password String Intentionally Omitted


Explanation of this level step-by-step
1. After logging in using the credentials from the prv level, it just gave me this msg ---> WELCOME TO THE UPPERCASE SHELL
>>
2. Upon investigating using ai found out that The game creators have swapped your regular Bash shell with a script that takes whatever you type and immediately converts it into **CAPITAL LETTERS** before running it.

If you type `ls`, the shell turns it into `LS`. Because Linux is case-sensitive, it looks for a program named `LS` in all capital letters, fails to find it, and throws an error. Try typing anything right now, and you will see it instantly scream at you in uppercase

**The Weakness in the System**

Look closely at the list of suggested commands: **`sh`** and **`man`**.

In Linux, **`$0`** is a special built-in variable that holds the name of the currently running program or shell. But there is an even more famous trick involving **positional parameters** and special environment handling in basic shells.

When a terminal prompt acts weirdly, it is often just a wrapper script _running over_ a standard shell. The simplest way to bypass an uppercase converter is to trigger an action or use a built-in shell feature that doesn't care about capitalization, or use an escape trick that spawns a raw terminal.

**The Magic Keystroke Trick**

In many interactive custom shells, **special characters** are not converted to uppercase because they don't have an uppercase version!

Try typing just this special variable parameter directly at your `>>` prompt and hit **Enter**

as suggested i used the special variable $0 and hit enter, now the terminal displays $ instead of >>

**Why this works:**

`$0` tells the underlying environment to execute the current command processor or execution context. Because it consists of a dollar sign and a number, the uppercase converter cannot alter it. It passes right through the filter and drops you directly into a normal, classic **`sh`** (Bourne Shell) prompt!

I've successfully shattered the uppercase cage. That simple **`$`** prompt means you are now running a raw, completely unrestricted **`sh`** terminal.

Since you are completely free from the uppercase filter, all standard Linux commands will now work exactly as they normally do.

now i'm back with the terminal so i used cat /etc/bandit_pass/bandit33 cmd
to read the pwd for next level & it successfully gave me the pwd, then ctrl+d to exit shell & again ctrl+d to exit the uppercase shell as well











SOC angle: The $0 variable escape technique is a 
classic restricted shell bypass. In real-world 
penetration testing and red team operations, 
attackers use special characters and shell 
built-in variables to escape restricted environments 
because they bypass input filters that only look 
for alphabetical commands. GTFOBins documents 
many such techniques. SOC analysts investigating 
compromised Linux systems should check shell history 
for $0, $SHELL manipulation, and similar bypass 
attempts as indicators of privilege escalation.