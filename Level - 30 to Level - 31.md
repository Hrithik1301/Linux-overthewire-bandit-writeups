

Didn't use ssh for this level, but used the pwd below to clone the git repo

Password String Intentionally Omitted (pwd)


## Level Goal

There is a git repository at `ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo` via the port `2220`. The password for the user `bandit30-git` is the same as for the user `bandit30`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

## Commands you may need to solve this level

git

## Helpful Reading Material

- [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)


hrithik@Hrithik:~$ git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
Cloning into 'repo'...
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit30-git@bandit.labs.overthewire.org's password:
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (4/4), 299 bytes | 33.00 KiB/s, done.
hrithik@Hrithik:~$ mv repo repo30
hrithik@Hrithik:~$ ls
repo27  repo28  repo29  repo30  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ cd repo30
hrithik@Hrithik:~/repo30$ ls
README.md
hrithik@Hrithik:~/repo30$ cat README.md
just an epmty file... muahaha
hrithik@Hrithik:~/repo30$ git log
commit 929c564cd34ca667773e2eb02f74b514bc4eeebf (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:25 2026 +0000

    initial commit of README.md
hrithik@Hrithik:~/repo30$ git show
commit 929c564cd34ca667773e2eb02f74b514bc4eeebf (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:25 2026 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..029ba42
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+just an epmty file... muahaha
hrithik@Hrithik:~/repo30$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
hrithik@Hrithik:~/repo30$ git tag
secret
hrithik@Hrithik:~/repo30$ git show secret
Password String Intentionally Omitted 




Explanation of this level step-by-step
1.  used  git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo as per level goal, to clone the repo, it worked, to avoid any further level complications 
2. renamed this level's repo to repo30 using mv repo repo30
3. used cd to get inside the repo30 directory
4. then ls revealed README.md file only
5. used cat README.md which gave a msg just an epmty file... muahaha
6. used all the git commands learned till now, but no cmd revealed anything related to the pwd, except for the git tag cmd which gave something called secret
7. upon investigating what it is using ai, it gave the below explanation

What is a Git Tag and How to Read It?

In Git, a **tag** is like a permanent sticky note attached to a specific moment in the project's history. Developers usually use them to mark major versions (like `v1.0.0`), but security professionals or developers can also use them to bookmark hidden snapshots.

To look inside the tag and see what information it contains, you use the **`git show`** command followed by the tag's name.

so used "git show secret" cmd & it actually gave the pwd for the next level






SOC angle: Git tags are used in real environments to 
mark release versions and deployment points. During 
IR on a compromised repository, checking git tags 
is a standard step — attackers sometimes tag 
malicious commits to make them appear as legitimate 
version releases, or developers accidentally tag 
sensitive snapshots. The git show <tagname> command 
is a direct forensic tool.


