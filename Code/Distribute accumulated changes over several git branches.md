# Distribute accumulated changes over several git branches

##### Metadata
created:: 2023-12-15 17:28
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform::
***

If you have accumulated a backlog of heterogenous changes on your branch (shame on you) and you need to switch to a different branch, you have a few options:

1. Ideal option: Don't put yourself in this situation! Commit early and often. And create unique branches for unique features you want to develop.
2. Easiest option: `git stash` 
3. Another option: commit your changes and then checkout

## Git Stash
 
 Pro Git chapter on stashing and cleaning: <a href="https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning">LINK</a>

 To stash all the current uncommitted changes, use `git stash --all`

 To see the list of current stashes, use `git stash list`. This will give you something like the following:
 ```
stash@{0}: WIP on master: 012345a Create README
stash@{1}: WIP on master: 012345b Refactor model notebook
stash@{2}: WIP on master: 012345c Add cont enrollment queries
 ```

 You can then switch branches and apply any of these stashes. For example: `git stash apply stash@{2}`
 
 This keeps the stash in the stack, however. If you want to immediately drop it from the stack after applying it, use `git stash pop stash@{2}`


## Git Checkout

If the changes are relevant to the branch, you can always just commit them locally and checkout to the new branch. If the commit includes a large amount of heterogenous changes, you can always go back and clean up the commit history before pushing to remote. 

See [[Grab file from another git branch]].