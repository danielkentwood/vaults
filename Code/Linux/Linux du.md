mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

# Find the size of folders in your directory

	du -h --max-depth=1 <folder name>

or just

	du -sh <folder name>/*

To get the size of all folders in the home directory, along with all subfolders one level down:

	du -h --max-depth=2 ~

And if you want to sort the output by size:

	du -h --max-depth=1 ~ | sort -hr

if you want to list the 20 biggest files in your directory (searching recursively): 

	du -ah ~/ | grep -v '\s/[^.]*$' | sort -rh | head -20
