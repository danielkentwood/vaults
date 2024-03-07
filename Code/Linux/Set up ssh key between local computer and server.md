mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

### Create ssh key on your local computer:
Check if you have an existing ssh key on your local computer: 

	ls -al ~/.ssh

If you have one of the following, you're set:
	-   _id_rsa.pub_
	-   _id_ecdsa.pub_
	-   _id_ed25519.pub_
If not, you'll need to create one:

	ssh-keygen -t rsa -C "your_email@aetna.com"

(you can use the default filename and you can leave the passphrase empty)
	
This will create a private and public key on your local computer, located at ~/.ssh/

You can see the public key contents with

	cat .ssh/id_rsa.pub

### Copy the public ssh key to the target location 
##### Using copy/paste
* copy the contents of `.ssh/id_rsa.pub` to your clipboard
* append the public key contents to `~/.ssh/authorized_keys` 


##### Using `ssh-copy-id`:
With your a-ID and edge node, execute the following.

	ssh-copy-id a522860@xhadrevrm7p

This will copy the public key to the server, located at ~/.ssh/

##### Permission errors
If you ever get an error about permissions being too open:
* The permissions of the private key (local computer) should be 600
* The permission of the public key (server) should be 644
* The permission of the ssh folder (both locations) should be 700
