

Didn't use ssh for this level, but used the pwd below to clone the git repo

Password String Intentionally Omitted (pwd)


## Level Goal

There is a git repository at `ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo` via the port `2220`. The password for the user `bandit29-git` is the same as for the user `bandit29`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

## Commands you may need to solve this level

git

## Helpful Reading Material

- [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)


hrithik@Hrithik:~$ git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
Cloning into 'repo'...
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit29-git@bandit.labs.overthewire.org's password:
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
hrithik@Hrithik:~$ ls
repo  repo27  repo28  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ mv repo repo29
hrithik@Hrithik:~$ ls
repo27  repo28  repo29  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ cd repo29
hrithik@Hrithik:~/repo29$ ls
README.md
hrithik@Hrithik:~/repo29$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>

hrithik@Hrithik:~/repo29$ git show
commit a9c5d1c2b43890809f3077bb9ec65c30ced242fb (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:08 2026 +0000

    fix username

diff --git a/README.md b/README.md
index 2da2f39..1af21d3 100644
--- a/README.md
+++ b/README.md
@@ -3,6 +3,6 @@ Some notes for bandit30 of bandit.

 ## credentials

-- username: bandit29
+- username: bandit30
 - password: <no passwords in production!>
hrithik@Hrithik:~/repo29$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
hrithik@Hrithik:~/repo29$ git tag
hrithik@Hrithik:~/repo29$ git checkout dev
branch 'dev' set up to track 'origin/dev'.
Switched to a new branch 'dev'
hrithik@Hrithik:~/repo29$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: Password String Intentionally Omitted

hrithik@Hrithik:~/repo29$ git checkout sploits-dev
branch 'sploits-dev' set up to track 'origin/sploits-dev'.
Switched to a new branch 'sploits-dev'
hrithik@Hrithik:~/repo29$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>



Explanation of this level step-by-step
1.  used  git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo as per level goal, to clone the repo, it worked, to avoid any further level complications 
2. renamed this level's repo to repo29 using mv repo repo29
3. used cd to get inside the repo29 directory
4. then ls revealed README.md file only
5. used cat README.md but it said <no passwords in production!>
6. so as usual i used ai to know why this happened, then it said
7. as you can see, the previous commit only fixed a typo in the username from `bandit29` to `bandit30`. The password isn't hidden in the master branch's commit history this time.
8. **The New Mechanic: Git Branches & Tags** %%explained this concept to me%%

In real-world software development, developers don't just work on one single line of history (called the `master` or `main` branch). They create **alternate dimensions of code** to test new features. These are called **branches** or **tags**.

A developer might have written the real password in a completely different branch or tagged a specific version of the project before cleaning up the `master` branch for production.

**How to Check Alternate Timelines**

Inside your `~/repo29` folder, use these two commands to see if there are hidden branches or version tags lying around:

1. Check for Secret Branches

By default, `git branch` only shows your current local branch. To see **all branches** (including the ones still sitting on the remote game server), i used "git branch -a" which gave the following output
Look for anything that isn't `master` or `remotes/origin/HEAD`

* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev

found two secret alternative timelines hidden on the server:

- **`remotes/origin/dev`** (a development branch)
- **`remotes/origin/sploits-dev`** (a exploits-development branch)

2. Check for Secret Tags

Developers use tags to mark specific release versions (like `v1.0`, `secret`, etc.). To see a list of all tags in this repository, used "git tag" as well which returned nothing

The `git tag` command came up completely empty, which tells us the password is definitely hiding inside one of these two development branches.


**How to Switch Timelines (Branches)**

To look inside a remote branch, you use the **`git checkout`** command followed by the name of the branch. This will instantly swap out the files in your current folder with the versions saved in that specific branch.

git checkout dev

Once Git switches you to the `dev` branch, the `README.md` file will automatically update itself to whatever text was saved in that timeline
next i used cat README.md to read the file & it gave me the pwd for next level, checked the other branch as well i.e., git checkout sploits-dev & cat README.md but it didn't give me anything






SOC angle: Git branches are commonly used by developers 
to hide or stage sensitive work. During security 
assessments and IR investigations, analysts check all 
branches of a compromised repo — not just the main 
branch — because attackers or careless developers 
may have left credentials, backdoors, or sensitive 
data in development or feature branches that never 
made it to production.










