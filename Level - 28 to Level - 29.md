

Didn't use ssh for this level, but used the pwd below to clone the git repo

Password String Intentionally Omitted (pwd)


## Level Goal

There is a git repository at `ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo` via the port `2220`. The password for the user `bandit28-git` is the same as for the user `bandit28`.

From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

## Commands you may need to solve this level

git

## Helpful Reading Material

- [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)



hrithik@Hrithik:~$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
fatal: destination path 'repo' already exists and is not an empty directory.
hrithik@Hrithik:~$ mv repo repo27
hrithik@Hrithik:~$ ls
repo27  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
Cloning into 'repo'...
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit28-git@bandit.labs.overthewire.org's password:
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), done.
Resolving deltas: 100% (2/2), done.
hrithik@Hrithik:~$ ls
repo  repo27  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ mv repo repo28
hrithik@Hrithik:~$ ls
repo27  repo28  ssh.key  ssh.key17  sshkey.bandit26
hrithik@Hrithik:~$ cd repo28
hrithik@Hrithik:~/repo28$ ls
README.md
hrithik@Hrithik:~/repo28$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx

hrithik@Hrithik:~/repo28$ git log
commit 83d77407b76c9f86ac4e691a47618641c9d527ba (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    fix info leak

commit 13bbc4d2414ffe0439b8ee4f5e5c2949780cf4b3
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    add missing data

commit f3334fbccbf9446a6af88a3c71021c2f57163322
Author: Ben Dover <noone@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    initial commit of README.md
hrithik@Hrithik:~/repo28$ git show
commit 83d77407b76c9f86ac4e691a47618641c9d527ba (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Wed Jun 24 14:59:06 2026 +0000

    fix info leak

diff --git a/README.md b/README.md
index 42331d9..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: Password String Intentionally Omitted
+- password: xxxxxxxxxx



Explanation of this level step-by-step
1. used  git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo as per level goal gave me an error ---> fatal: destination path 'repo' already exists and is not an empty directory
2. so renamed the "repo" directory from prv level to repo27 using mv repo repo27
3. then used the git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo to clone the repo this time it worked, to avoid any further level complications 
4. again renamed this level's repo to repo28 using mv repo repo28
5. used cd to get inside the repo28 directory
6. then ls revealed README.md file only
7. used cat README.md but it masked the password for next level
8. used ai & found that git log & git show are the commands used to show the history of the repo directory
9. so used both to look at what results they produced, git log only gave the logs without revealing the contents of it
10. but, git show gave the contents of the commits & finally got the pwd for next level


**Commands explanation**:

- **`git log`**
    - **What it does:** This prints out a list of all the commits (saves) made to this repository. You will see commit IDs, the names of the authors, dates, and messages explaining what they changed. Look closely at the commit messages for clues about when the password was modified or hidden.
- **`git show`**
    - **What it does:** Once you see the commit history, you can use `git show <commit-id>` (or just `git show` by itself to look at the immediate previous changes) to see the exact lines of text that were added or deleted in that specific update.


**What `git log` Actually Is: The Diary Index**

Think of **`git log`** as the **Table of Contents** or the **Index** at the back of a history book.

It does not read the actual text lines inside your files. Instead, it only looks at the high-level summary metadata of each save point (commit). It answers questions like:

- _Who_ made the change?
- _When_ did they make it?
- _What headline summary_ did they write to describe it? (e.g., `"fix info leak"`).

Because `git log` only gives you a timeline list of names and summaries, it will never show you the internal line-by-line modifications or hidden text strings.


**What `git show` Actually Is: The X-Ray Diff**

On the other hand, **`git show`** is an **X-ray text viewer**. It inspects the literal contents of a commit.

When you run `git show` without adding anything else, it automatically defaults to looking at the very latest commit on the timeline (which was `"fix info leak"`). It prints out a **Diff** (differential overview) showing you a strict side-by-side comparison of what that specific commit did to the code:

- Lines marked with a red minus symbol (**`-`**) mean: _"This text used to exist right here, but this commit deleted it."_
- Lines marked with a green plus symbol (**`+`**) mean: _"This is the new text that was added to replace it."_

Because the commit message was literally _"fix info leak"_, `git show` pulled back the curtain and revealed that the author deleted the real password (`- password: Em7...`) and substituted it with the fake string (`+ password: xxx...`).


**Pro-Tip for Git Levels**

If you want to view a specific older commit rather than just the latest one, you can combine both tools! You grab a commit ID from your `git log` list (like `13bbc4d...`) and paste it right after the show command:

git show 13bbc4d2414ffe0439b8ee4f5e5c2949780cf4b3





SOC angle: Git commit history is forensic evidence. 
During incident response on a compromised developer 
machine or CI/CD pipeline, analysts use git log and 
git show to reconstruct what changed, when, and who 
made the change. A commit message like "fix info leak" 
is exactly the kind of suspicious activity that would 
trigger an investigation into what was leaked and whether 
it was accessed before being removed.





