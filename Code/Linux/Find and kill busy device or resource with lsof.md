mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

1.  Find the directory (or the closest parent directory) of the busy resource. Let's say it is ~/bin/
2.  Run the following at the command line

`lsof +D ~/bin`

This should find all running resources in that directory, and give you the pid of the resource(s).

1.  You can then search for information about the resource with the following (let's assume the pid is 138878):

`ps aux | grep 138878`

This will give you name of the program that is running the resource. If you can't kill the process by exiting the program, then proceed to the next step.

1.  Kill the resource with the following:

`kill -9 138878`

1.  If there are multiple resources attached to the same program (let's say it's chrome), you can use:

`killall -9 chrome`

### Dealing with .nfs files in HIVE
[[dealing with nfs files in HIVE]]

