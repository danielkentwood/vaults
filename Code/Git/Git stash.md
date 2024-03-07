mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform:: 

This [[git]] command allows you to stash uncommitted diffs, allowing you to switch branches.

Pro Git chapter on stashing and cleaning: <a href="https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning">LINK</a>

### To view the stack of stashes:

	git stash list

This will give you something like the following:
 ```bash
stash@{0}: WIP on master: 012345a Create README
stash@{1}: WIP on master: 012345b Refactor model notebook
stash@{2}: WIP on master: 012345c Add cont enrollment queries
 ```

### To view the diffs in a particular stash:

	git stash show -p stash@{0}

This will show you the contents of the most recent stash

### To stash all the diffs

	git stash

### To unstash all the diffs
If you want to just unstash the most recent stash:

	git stash pop

if you want to unstash a specific stash, let's say the third one in the stack:

	git stash pop stash@{2}

### To include untracked files in the stash:
[https://stackoverflow.com/questions/835501/how-do-you-stash-an-untracked-file](https://stackoverflow.com/questions/835501/how-do-you-stash-an-untracked-file)

	git stash --include-untracked

### Difference between `git stash pop` and `git stash apply`
[https://newbedev.com/difference-between-git-stash-pop-and-git-stash-apply](https://newbedev.com/difference-between-git-stash-pop-and-git-stash-apply)
Using 'pop' should remove the stash after applying it.
Using 'apply' will keep it in the stash stack.


### Drop a stash
Drop the most recent stash

	git stash drop

### Apply changes from just one file in the stash
You can use `git checkout` to do this. Let's say you want to apply a diff from `garbage_truck.py` in the second stash in the stack:

	git checkout stash@{1} -- garbage_truck.py