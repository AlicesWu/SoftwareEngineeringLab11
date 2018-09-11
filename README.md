### [➡️link to respository in github⬅️](https://github.com/AlicesWu/SoftwareEngineeringLab11)


# bash command
##### 1. Configure git in terminal(MacOS)
```bash
$ git config --global user.name AlicesWu
$ git config --global user.email imadream@foxmail.com
$ ssh-keygen -C imadream@foxmail.com -t rsa
$ cd ~/.ssh
$ cat id_rsa.pub # copy and paste to configuration about ssh in github
$ ssh -v git@github.com # set up connection to my github
```
##### 2. Set up my respository
Firstly build a new respository in my github.
```bash
$ cd ~/11510212/selab11
$ git init
$ git remote add origin git@github.com:AlicesWu/SoftwareEngineeringLab11.git
```
##### 3. Commit
```bash
# master
$ touch 1.c
$ git add 1.c
$ git commit -m "add 1.c"
$ touch 2.c
$ git add 2.c
$ git commit -m "add 2.c"
$ git push -u origin master
```
```bash
# branch1
$ git branch branch1
$ git checkout branch1
$ touch 3.c
$ git add 3.c
$ git commit -m "add 3.c to branch1"
$ touch 4.c
$ git add 4.c
$ git commit -m "add 4.c to branch1"
$ vim 1.c
$ cat 1.c
Make some changes to 1.c on branch1

$ git add 1.c
$ git commit -m "1.c was modified"
$ git push -u origin branch1
```
```bash
# back to master and merge branch1
$ git checkout master
$ touch 5.c
$ git add 5.c
$ git commit -m "add 5.c to master"
$ git merge branch1
$ git push -u origin master
```
```bash
# branch2
$ git branch branch2
$ git checkout branch2
$ touch 6.c
$ git add 6.c
$ git commit -m "add 6.c to branch2"
$ touch 7.c
$ git add 7.c
$ git commit -m "add 7.c to branch2"
$ vim 1.c
$ cat 1.c
Also make some different changes to 1.c on branch2

$ git add 1.c
$ git commit -m "1.c was modified in branch2"
$ git push -u origin branch2
```
```bash
# rebase
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: add 6.c to branch2
Applying: add 7.c to branch2
Applying: 1.c was modified in branch2
Using index info to reconstruct a base tree...
M	1.c
.git/rebase-apply/patch:7: new blank line at EOF.
+
warning: 1 line adds whitespace errors.
Falling back to patching base and 3-way merge...
Auto-merging 1.c
CONFLICT (content): Merge conflict in 1.c
error: Failed to merge in the changes.
Patch failed at 0003 1.c was modified in branch2
The copy of the patch that failed is found in: .git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
$ cat 1.c
<<<<<<< HEAD
Make some changes to 1.c on branch1
=======
Also make some different changes to 1.c on branch2.
>>>>>>> 1.c was modified in branch2
$ vim 1.c # delete the first, third, fifth line
$ git add -u
$ git rebase --continue
```
```bash
# merge branch2
$ git checkout master
$ git merge branch2
$ ls  # list files in master
1.c 2.c 3.c 4.c 5.c 6.c 7.c
$ cat 1.c
Make some changes to 1.c on branch1

Also make some different changes to 1.c on branch2.

```
```bash
# add final file
$ touch 8.c
$ git add 8.c
$ git commit -m "add 8.c to master"
$ ls
1.c 2.c 3.c 4.c 5.c 6.c 7.c 8.c
$ git push -u origin master
```

When I tried to rebase, I made a lot of mistake at first.

So I use these command to cover all code and commit in master and branch2.
```bash
# cover a branch from remote respository
$ git fetch --all  
$ git reset --hard origin/master # master can be other name of branch
$ git pull
```

```bash
# draw graph of all commits in this respository
$ git log --all --decorate --oneline --graph
```
### git log
```bash
$ git log > git.log
$ cat git.log
commit 5793b3592b4814b1f2f64644d1de267872be4523
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 22:19:22 2018 +0800

    add 8.c to master

commit bd012d293d428aa8fbdb9c187dab9b2d0a0bb954
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:49:13 2018 +0800

    1.c was modified in branch2

commit 9b5fdf12da12ce5ed87221f965c1d5468317da16
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:37:10 2018 +0800

    add 7.c to branch2

commit 90b859234b4073cdb01a88d446102c96fd65ba98
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:36:50 2018 +0800

    add 6.c to branch2

commit 3b0f22d144b214ba5b3b1d41855c988e7c6c56f2
Merge: 0319449 0e22dc6
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:44:12 2018 +0800

    Merge branch 'branch1'

commit 0e22dc6bacd6cbbf88109dbfdb30f8afbfb5ce0b
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:41:59 2018 +0800

    1.c was modified

commit 0319449b42290d7c52a8891ef8c627ae88a4b9ae
Merge: 245f6de 90d02ee
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 17:00:23 2018 +0800

    Merge branch 'branch1'

commit 245f6deca00c515bcfa9d6d9ed851064686d0afc
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 16:59:05 2018 +0800

    add 5.c to master

commit 90d02ee5631c698fc777f585942eebfd36b0828b
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 16:53:27 2018 +0800

    add 4.c to branch1

commit 99ad9bb32778fe0da6e15f062fc7a1e06b4a788c
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 16:07:00 2018 +0800

    add 3.c to branch1

commit 23b13a303c1e42ac9b41d406529d71e57b5ab839
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 16:03:00 2018 +0800

    add 2.c

commit c874dba6bf1176aab8c2544cdfe93f2313318aaa
Author: AlicesWu <imadream@foxmail.com>
Date:   Mon Jun 4 15:48:16 2018 +0800

    add 1.c
```
### How do I solve conflicts on second merge?
This is the conflict happen in 1.c. I simply delete line 1 and line 5, erase content in line 3, which are the labels of conflicts.

And then I continue rebasing, the conflict was solved.
![](https://raw.githubusercontent.com/AlicesWu/images_markdown/master/img_selab11report/conflict.png)

### Graph
![](https://github.com/AlicesWu/images_markdown/blob/master/img_selab11report/finalgrach.png?raw=true)
