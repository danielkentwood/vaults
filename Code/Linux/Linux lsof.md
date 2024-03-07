mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

### show all the listening ports that were opened by processes owned by me:

	lsof -nP -iTCP -sTCP:LISTEN | grep a522860

-   -n - Do not convert port numbers to port names.
-   -p - Do not resolve hostnames, show numerical addresses.
-   -iTCP -sTCP:LISTEN - Show only network files with TCP state LISTEN.

### show all ports that are already in use
Sometimes when you want to SSH onto the edge node, you need to specify a specific port. It is helpful to see which ports are already in use.

Run this command: 

    lsof -i -P -n

The output looks similar to this: 
```bash
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
process process ID root 3u IPv4 3011 TCP *:port (LISTEN)
process process ID root 3u IPv4 3011 TCP *:port (LISTEN)
...
```

If you want to kill all the processes on a specific port, you can use the following:

    kill -9 $PROCESS_ID