

Connecting to ssh level 26 using the credentials from Prv level


ssh bandit26@bandit.labs.overthewire.org -i sshkey.bandit26 -p 2220


## Level Goal

Good job getting a shell! Now hurry and grab the password for bandit27!

## Commands you may need to solve this level

ls




:set shell=/bin/bash
:shell

bandit26@bandit:~$ ls
bandit27-do  text.txt
bandit26@bandit:~$ ls -l
total 20
-rwsr-x--- 1 bandit27 bandit26 14880 Jun 24 14:59 bandit27-do
-rw-r----- 1 bandit26 bandit26   258 Jun 24 14:59 text.txt
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
Password String Intentionally Omitted

%%also obtained the pwd for bandit26 using cat /etc/bandit_pass/bandit26 cmd ---> Password String Intentionally Omitted%%



Explanation of this level step-by-step
1. used ssh bandit26@bandit.labs.overthewire.org -i sshkey.bandit26 -p 2220 ---> logged me out immediately
2. upon investigation using ai i found out that i need to minimize the shell window to the maximum and ---> run the logging cmd
3. then it freezes at more ---> then i need to hit "v" to open a vi editor
4. then type :set shell=/bin/bash ---> enter
5. then :shell ---> enter
6. then the shell for bandit26 opens ---> then ls ---> gave me a SUID file bandit27-do
7. then ./bandit27-do cat /etc/bandit_pass/bandit27 ---> gave me the pwd for next level



**The Story Behind This Level**

Normally, when you successfully log into a Linux user account via SSH, the server drops you into a **shell** (which is almost always **`/bin/bash`**). Bash is a friendly program that sits there waiting for you to type commands like `ls`, `cd`, or `cat`.

However, the creator of `bandit26` did something sneaky. They went into the system settings and changed `bandit26`'s default shell.

Instead of opening `bin/bash`, logging into `bandit26` triggers a **custom script or text viewer program**. The second that custom program finishes running or reading, it instantly logs you out and terminates your connection.

**The Clue in the Commands: `more` and `vi`**

Look closely at the suggested commands: **`more`** and **`vi`**.

- **`more`** is an old-school text reader tool. If a text file is too long to fit on your terminal monitor, `more` pauses the screen at the very bottom and waits for you to press keys to scroll down.
- **`vi`** is a text editor.

If the custom shell script happens to use a tool like `more` to display a message, it creates a golden opportunity. If you can make your terminal window **really small** before you log in, `more` will be forced to pause because the text won't fit on your tiny screen.

While `more` is paused, it accepts special keyboard shortcuts. One of those shortcuts lets you instantly launch a text editor like **`vi`**, and inside `vi`, you can type a command to force the system to give you a normal Bash shell!

**What happens:** Your screen will change completely. It will open the text inside the classic `vi` editor. You will see a bunch of tilde (`~`) characters lines down the left side.

then type :set shell=/bin/bash then hit enter

Every time you are inside a text editor like `vi`, the editor is sitting inside the environment of the current user (`bandit26`)
If `vi` needs to run an external command or open an inner command prompt for you, it looks at a built-in configuration setting called **`shell`** to know which program to launch
- By default, `vi` inherits the broken, custom shell script that the game creators assigned to `bandit26`.
- If you tried to launch a terminal straight away, `vi` would try to open that custom script, the script would instantly exit, and you would be logged out immediately
By typing **`:set shell=/bin/bash`**, you manually forced the text editor to overwrite its internal settings. You told it: _"Hey `vi`, if I ask you to open a command prompt, ignore the default system shell and use the real, unrestricted **`/bin/bash`** instead._

then type :shell and hit enter

Once you successfully changed `vi`'s target map to point to Bash, you needed to tell it to pull the trigger.

The command **`:shell`** is an internal `vi` feature that tells the editor: **"Pause the text editing screen for a moment, open up a sub-process terminal, and drop the user into a live command prompt**"

Because you pre-configured the editor to use `/bin/bash` in the previous step, `vi` spun up a perfectly working, fully unrestricted Bash terminal using `bandit26`’s account privileges. You effectively tunneled _underneath_ the restrictive script that was trapping you at the login door.

now as we are in the shell environment type ls & ls -l for the SUID file bandit27-do for file permissions, then type "./bandit27-do cat /etc/bandit_pass/bandit27" cmd for the password

**How do you exit the `vi` editor**
Right now, your active shell is technically a "child process" running inside `vi`. To clean up your workspace or log out correctly, you need to know how to close the layers:

Step A: Close the Bash Prompt

When you are completely finished running commands in your new terminal prompt, type **`exit`** and hit **Enter**.

- **What this does:** This closes the shell subprocess and drops you right back inside the frozen `vi` text window where you started

Step B: Close the `vi` Text Editor

Once you are back inside the `vi` editor screen (where you see the text lines and tildes `~`), you can close the editor entirely using standard `vi` quit commands:

Type **`:q!`** and hit **Enter**.

- **Mechanics:** The `:` enters command mode, `q` stands for quit, and the `!` forces it to exit instantly without trying to save any accidental changes

(Note: Because the `vi` editor was originally spawned by that restrictive login script, closing `vi` completely will finish the script and instantly disconnect your SSH session. That is perfectly normal!)




SOC angle: The vi/vim text editor escape technique is 
a well-known privilege escalation and shell escape 
method listed on GTFOBins (gtfobins.github.io) — 
a reference database of Unix binaries that can be 
abused to bypass security restrictions. SOC analysts 
and IR teams check GTFOBins during investigations 
to understand how attackers may have escalated 
privileges on a compromised system.