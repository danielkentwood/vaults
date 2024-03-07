mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform:: 

## Switch to a Branch That Came From a Remote Repo

To get a list of all branches from the remote, use [[git branch]]:

	git pull
	git branch -r

Run this command to switch to the branch:

	git checkout --track origin/my-branch-name

From: [https://www.nobledesktop.com/learn/git/git-branches](https://www.nobledesktop.com/learn/git/git-branches)

