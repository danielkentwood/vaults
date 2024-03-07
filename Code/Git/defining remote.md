mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform:: 

# set the upstream branch

In order to [[git pull]], you need to set up your upstream branch. This is typically the remote version of the branch that you're developing. (You can always do "git pull origin master" to pull the most recent changes from master)

The easiest way to do this is the following, when you first commit:

`git push -u <remote> <branch>`
For example:
`git push -u origin new_feature`

Otherwise, this can be done at any time:

`git branch --set-upstream-to=origin/<remote_branch> $local_branch_name`

# see the upstream repo and branch
to see the upstream repo and branches:

	git remote show origin

# add a new remote
`origin` is the default remote repo, but it doesn't need to be the only one.
You can add any number of remote repos with `git remote add <new_remote_name> git@github.aetna.com:<account>/<repo>.git`.

You can push to any one of them with `git push <new_remote_name> <target_branch>`.

# for switching between https and ssh remote
https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories

`git remote set-url origin git@github.com:USERNAME/REPOSITORY.git`