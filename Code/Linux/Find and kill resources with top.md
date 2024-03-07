mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

# How to view (and kill) running jobs

### Viewing jobs

In order to view the currently running jobs and their stats, use:

    top -U $USER

This will give a real-time view of the running processes. Another useful command that provides a more static view of the currently running processes is `ps`. For example:

    ps au

This will give output similar to below:
```bash
USER      PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
root    52859   0.0  0.0  4480012   3648 s001  Ss   14Jul21   0:00.08 login -pf a522860
a522860 53305   0.0  0.0  4423744   1064 s000  S+   Thu09AM   0:00.02 bash
a522860 53302   0.0  0.0  4410300   1028 s000  S    Thu09AM   0:00.05 -ksh
root    53301   0.0  0.0  4505612   3668 s000  Ss   Thu09AM   0:00.90 login -pf a522860
a522860 50717   0.0  0.0  5305428   2248 s001  T    Thu08AM   0:00.16 ssh xhadrevrm7p -L 8888:localhost:8888
```


### Killing jobs/processes

In order to kill all jobs running from a certain user id, running within a conda environment:

```bash
for p in `ps -ef | grep $USERID | grep conda| awk '{print $2}'`; do kill -9 $p; done
```

You can continue to add grep pipes to narrow down the scope of what you want to kill.

