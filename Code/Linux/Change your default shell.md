mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

For example, if your default shell is zsh and you want it to be bash:

	chsh -s /bin/bash

I had to do this to get terminal to startup in bash so that the .bash_profile would be executed on startup, which was necessary for conda to run after installation.