mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]], [[SQL]]
platform:: [[Hadoop]], [[Hive]]

### .nfs files in Hive
When a file that is currently open on an NFS client is closed, the NFS client will rename the file as .nfsXXXXX to discourage other clients/processes from using it. But since you can't delete the file directly, it can lock up a git branch. This happens regularly. 

1. Use `lsof` to search for the .nfs file
```bash
lsof ./.nfs00000000d3c021e800000747
```

This should give you the pid
```bash
COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF       NODE NAME
java    172408 a522860  512r   REG   0,41    13397 3552584168 ./.nfs00000000d3c021e800000747
```

2. kill the pid
```bash
kill -9 172408
```



