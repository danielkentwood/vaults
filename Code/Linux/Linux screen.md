mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

First, ssh in to the edge node

`ssh xhadrevrm7p`

Then, start bash.

Then, check to see if you already have a screen session assigned to your task (let's assume jupyter):

`screen -list`

If it does exist, reattach by using the session ID (in the list above):

`screen -r {session_id}`

If a session doesn't exist, create one:

`screen -S session_name`

And then fire up your task (e.g., the jupyterlab instance):

`jupyter lab --ip xhadrevrm7p --port 23456 --ServerApp.iopub_data_rate_limit=1.0e10`

### OTHER COMMANDS

To detach from session:

`Ctrl+a, d`

To delete a session:

`screen -X -S [session ID] quit`

To rename a session:

`screen -S [session ID] -X sessionname [new session name]`

REFERENCE:

[https://linuxize.com/post/how-to-use-linux-screen/](https://linuxize.com/post/how-to-use-linux-screen/)

