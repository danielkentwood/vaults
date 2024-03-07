# Notes on coding w Tomas

Created: August 25, 2020 5:15 PM
Updated: September 17, 2020 11:29 AM



### BASH

Some common functions:

```
grep

```

will search the contents of files for a search term

```
seq 1 10 

```

this produces a sequence of numbers

```
ls -la

```

This shows all the contents of a directory with the permission

```
tac

```

this reverses the order of a list

```
!!

```

Auto expand to the previous command. For example:

```
rm script.sh
sudo !!

```

This would be: sudo rm script.sh

```
su

```

this switches the current user

```
whoami
```

this tells you who the current user is

```
ps -a
```

prints a list of processes running on the computer



### **GIT**

Topic branch: a new branch where you are developing a new feature

If you get conflict, you can do git status to check out info about it.

`git merge --abort`

 to stop the merge

HEAD: this is where you currently are in your code status

Adding is putting the changes into the staging phase

Concept - a tree

```
Git shortlog
```

What does shortlog do?

Tig is a program that gives you a terminal interface to Git

```
git checkout master

```

switch to the master branch

```
git checkout -b newbranch

```

create new branch and switch to it

```
git diff

```

show all changes on the current branch that modify the files that are tracked by git, and are not committed

```
git diff -staged

```

show changes in the staging area

```
git status

```

which files are in which stage

```
git reset HEAD

```

What does this do?

```
git restore --staged README.rst

```

restores the README.rst file from the staged phase

Staging

What if you have multiple changes and you're not sure if you want to stage them all?

```
git add -p

```

Tracking commits

```
git log

```

shows the history of commits with details

```
git blame

```

shows you all of the commits that included changes for a particular file

What if I want to find commits that changed a particular method or line in the file?

```
git log -p -S'self.replace()'

```

this will search the log for all of the commits that changed something with self.replace()

What about when you have commits that you want to reverse?

```
git reset HEAD~1

```

This puts the last commit back into the diff

```
git reset —hard -HEAD~1

```

This doesn’t bring the last commit to diff, it just erases it.

Rebasing? This puts the latest changes in the main repository on the bottom of your current branch.

```
git rebase master

```

If there is a conflict, this will initiate the resolution process

```
git pull —rebase master

```

What specifically does this do?

```
git reflog

```

what does this do?

```
git cherrypick

```

what does this do?

Important skill: consolidating commits and using interactive rebase to alter the git history of your branch to make it more presentable.

```
git rebase -i master

```

This will introduce an interactive mode for rebasing.

You don't have to actually be rebasing. You can also just use it to change the messages in the commits (if they are messed up or insufficient).

You can also change the order of the commits and let you merge them.

```
git branch

```

see all current branches

```
git branch -D branch_name
git push origin :branch_name

```

delete the specified branch locally and then at the remote source