mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

[https://www.geeksforgeeks.org/ps-command-in-linux-with-examples/](https://www.geeksforgeeks.org/ps-command-in-linux-with-examples/)
https://www.tecmint.com/ps-command-examples-for-linux-process-monitoring/


# Useful commands

### Show all processes owned by me

`ps -x`

This will give a list of all of the processes owned by you (root). It is identical to:

`ps -G root`

…which shows all processes for the "root" group ID.

If you want to get more detail and show the parent-child relationships between processes, you can run:

`ps -xf`

Where the -f flag shows you the full format


### Kill all jobs running from me

`for p in ps -ef | grep a522860 | grep conda| awk '{print $2}'; do kill -9 $p; done`

This will get the full details of all currently running jobs, search them for my aID, search them for any mention of conda, grab the second item in each row (the PID), and then cycle through those PIDs to kill them (the -9 flag is forced termination). You can continue to add pipes to narrow down the scope of what you want to kill.

### Return only one value from the results
For example, if you only want the id of the owner of the process on a specific port:

	ps -ef | grep :$CUR_PORT | awk '{print $1}'

If you want the pid of a process owned by you on a specific port:

	ps -xf | grep :$CUR_PORT | awk '{print $2}'