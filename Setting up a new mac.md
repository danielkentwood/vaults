# Setting up a new mac

##### Metadata
created:: 2023-08-10 22:53
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis #aetna 
kind:: #zettel 
status:: #status/seed
parent:: 
***


* Log in to the following:
	* Teams
	* Outlook
		* Go to settings and make sure your signature is set up
	* Chrome (Aetna account) -- allow sync and make default browser
	* OneDrive
* Download the following:
	* Obsidian
		* Point it to the backed up vault on OneDrive, and ensure it is synchronizing
	* VS Code
		* [[VS Code set up remote environments]]
			* The `ssh_config` file in step 5 is saved in your OneDrive main directory. Just copy it over. 
	* Command Line Tools from XCode (you'll be prompted to install this during the setup of VS Code -- Python Intellisense plugin)
	* anaconda
		* after it is installed, run the following commands 
```bash
source ~/anaconda3/bin/activate
conda init
conda config --set auto_activate_base True
```


* Do the following
	* [[Set up ssh key between local computer and server]]
	* [[Set up ssh key between local computer and Github]]
	* Set up renewing [[ç Kerberos]] ticket on edge node
	* Create .bashrc file in local home folder
		* copy the bashrc from the edge node and use that, with small modifications
	* in .bashrc, set up aliases for connecting to edge nodes with ssh:
		```bash
alias 2p="ssh xhadrevrm2p"
alias 4p="ssh xhadrevrm4p"
alias 5p="ssh xhadrevrm5p"
alias 7p="ssh xhadrevrm7p"
alias 16p="ssh xhadrevrm16p"
		```
		*  after .bashrc is saved, run `source ~/.bashrc` to refresh the terminal and implement the changes.
	* Launch jupyter lab in a [[Linux screen]] session, then in the Chrome browser, go to the three dots --> More Tools --> Create Shortcut
	