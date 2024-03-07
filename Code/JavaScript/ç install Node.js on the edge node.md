# ç install Node.js on the edge node

##### Metadata
created:: 2023-03-16 17:07
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[JavaScript]]
platform:: [[Conda]]
***

Due to the fact that users don't have super user permissions on the edge node, it is impossible (or at least really really hard) to install node via the usual methods of
1. package installer (apt, homebrew, etc)
2. official installer from website
3. node version manager (NVM)

All of these require SU privileges at some point in the process.

Instead, you can use `conda`. 

Start with a fresh env:
```bash
conda create --name nodejs python=3.9
```

Then have node be the first thing that you install:
```bash
conda install nodejs
```

Assuming this works (it did for me), you can check versions with the following:
```bash
node --version
```
and 
```bash
npm --version
```
