
## Level Goal

The password for the next level is stored in a file called **-** located in the home directory

## Commands you may need to solve this level

[ls](https://manpages.ubuntu.com/manpages/noble/man1/ls.1.html) , [cd](https://manpages.ubuntu.com/manpages/noble/man1/cd.1posix.html) , [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html) , [file](https://manpages.ubuntu.com/manpages/noble/man1/file.1.html) , [du](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html) , [find](https://manpages.ubuntu.com/manpages/noble/man1/find.1.html)


so i logged into level - 2 using the following cmd
ssh bandit1@bandit.labs.overthewire.org -p 2220 with the pwd generated in prv. level, 
and after following the instructions in the website i used "ls" cmd to view the contents of the home directory and it showed only a file with name "-"

but using  " cat - " cmd
gave me nothing but a blinking cursor

upon inspection i also used  " cat -- - " cmd
still the same response
so i asked claude to give me a brief description of the url's provided in the lvl 2 webpage it gave 

Special characters in Linux** — some characters like `-`, `/`, `*`, `.` have **special meanings** to the terminal. They're not treated as normal letters.

**`-` specifically** → Linux treats a lone dash as "read from keyboard input" (stdin), not as a filename. That's why `cat -` just sits waiting.

**`./`** means "current directory" → it forces Linux to treat what follows as a **file path**, not a special character.

So `./` is the way to say "look here, in this folder, for a file."


and upon entering the following command it gave the pwd to the next level

cat ./- 

Password String Intentionally Omitted



SOC angle: Attackers name malicious files with special characters 
like - or spaces to confuse automated scanners and analysts 
who don't know how to handle them.