# ç Creating a new graph with Aetna data
created:: 2022-06-26 16:36
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[TigerGraph]], [[Docker]]
***

1. Build a docker container using the Tigergraph image
```bash
DOCKER="adrd"
SOURCE_PATH="${PWD}/data"

docker run -d \
	-p 14022:22 \
	-p 9000:9000 \
	-p 14240:14240 \
	--name $DOCKER \
	--ulimit nofile=1000000:1000000 \
	-v $SOURCE_PATH:/home/tigergraph/adrd \
	-t docker.tigergraph.com/tigergraph:latest
```

2. Log in to the container
```bash
ssh -p 14022 tigergraph@localhost
```

NOTE: If you attempt to log in and get this error:

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:6VVlewTZUdbXRe22c0RpkzKaNI8GnWOrsp9/2M1XAG4.
Please contact your system administrator.
Add correct host key in /Users/a522860/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/a522860/.ssh/known_hosts:7
ECDSA host key for [localhost]:14022 has changed and you have requested strict checking.
Host key verification failed.
```

... it is likely because you already have a line in your `.ssh/known_hosts` file that starts with `[localhost]:<the port you just tried to log in to>` and it happens to be a different host key (e.g., maybe you downloaded a different docker image and tried to build and log in to a different container with this port, so it saved that key for this port). To fix this, you can either manually remove the offending line from your known_hosts file (hint: the warning message will tell you which line the offending key is on), or you can use the following line (assuming the port you are connecting to is 14022):

```
ssh-keygen -R [localhost]:14022
```

3. Start graph studio
```bash
gadmin start all
```

4. Build your graph schema

5. Get the data
	1. Pull data from hadoop
	2. Export to .csv 
	3. Store the .csv files in the data folder that is mapped to the docker image

6. Upload the data to the graph



## Helpful Resources
* TigerGraph "getting started with docker" doc:  https://docs.tigergraph.com/tigergraph-server/current/getting-started/docker
* Best practices for modeling data with a graph database
	* https://www.youtube.com/watch?v=S9uXNlKJZyI
	* For modeling time series: https://youtu.be/S9uXNlKJZyI?t=1665