mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

### Set up OneDrive on local computer
(This allows you to work with files that are automatically backed up by the cloud)

### ![[Set up ssh key between local computer and server]]

### Use scp to copy your local file to the server:
	scp -i ~/.ssh/id_rsa ~/OneDrive\ -\ CVS\ Health/TODO.xlsx a522860@xhadrevrm7p:~/TODO/TODO.xlsx

