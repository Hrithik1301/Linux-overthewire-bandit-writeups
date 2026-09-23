
Didn't use ssh for this level, but used the pwd below to clone the git repo

Password String Intentionally Omitted


## Level Goal

There is a git repository at `ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo` via the port `2220`. The password for the user `bandit27-git` is the same as for the user `bandit27`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

## Commands you may need to solve this level

git

## Helpful Reading Material

- [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)



hrithik@Hrithik:~$ sudo apt update
[sudo: authenticate] Password:
Hit:1 http://security.ubuntu.com/ubuntu resolute-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu resolute InRelease
Hit:3 http://archive.ubuntu.com/ubuntu resolute-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu resolute-backports InRelease
163 packages can be upgraded. Run 'apt list --upgradable' to see them.
hrithik@Hrithik:~$ sudo apt install git -y
git is already the newest version (1:2.53.0-1ubuntu1).
Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 163
hrithik@Hrithik:~$ git --version
git version 2.53.0
hrithik@Hrithik:~$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
Cloning into 'repo'...
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit27-git@bandit.labs.overthewire.org's password:
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
hrithik@Hrithik:~$ ls
repo  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ cd repo
hrithik@Hrithik:~/repo$ ls
README
hrithik@Hrithik:~/repo$ cat README
The password to the next level is: Password String Intentionally Omitted



Explanation of this level step-by-step
1. after using the below commands sudo apt update, sudo apt install git -y, git --version %%asked for authentication at the first cmd itself%%
2. got the package list updated along with the git version installed on my local machine
3. then used git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo to clone the repo mentioned in the level goal
4. then used ls cmd to verify if the repo is cloned or not
5. then used the cd command to look inside the repo ---> cd repo %%the cloned repo name is also repo%%
6. then typed ls to look inside the contents of the repo ---> only one file named README
7. used cat README ---> to read the contents of README file ---> it then revealed the password for the next level

Below is the explanation for the cmd ---> git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo

**The Tool & Action**

- **`git`**: This calls the version control software you just installed.
- **`clone`**: This is the specific action. It means _"make an exact, identical duplicate copy of the remote folder and download it here."_

**The URL (Where to find it)**

1. **`ssh://`**: This tells Git to use a secure network tunnel (**Secure Shell**) to communicate with the server so no one can sniff your data.
2. **`bandit27-git`**: This is the specific **user account** name you are using to access the repository.
3. **`@`**: This simply connects the user to the server address (just like in an email address).
4. **`bandit.labs.overthewire.org`**: This is the domain name of the OverTheWire **host server** where the game files live.
5. **`:2220`**: This tells Git to connect using **Port 2220**. By default, SSH tries to connect to port 22, but the game creators moved it to 2220 to avoid standard traffic.
6. **`/home/bandit27-git/repo`**: This is the exact folder path **inside** the server where the project files are physically stored.




SOC angle: Git repositories are a major source of 
credential leaks. Developers accidentally commit 
API keys, passwords, and private keys to repos — 
sometimes public ones on GitHub. Tools like truffleHog 
and git-secrets scan repos for leaked credentials. 
As a SOC analyst you may be asked to investigate 
alerts triggered by credential scanning tools 
detecting secrets in internal or public repos.
