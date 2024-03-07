mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform:: 

Assume the filename is server.js, and assume you are currently in the local branch where you want to bring/replace the file (NOTE: this will force overwrite the file if it already exists).

If the file version that you want is on a remote branch called dev:

	git checkout origin/dev server.js

If the file version that you want is on a local branch called dev:

	git checkout dev server.js


### External 
Here is an article on how to do this: <a href="https://jasonrudolph.com/blog/2009/02/25/git-tip-how-to-merge-specific-files-from-another-branch/">LINK</a>