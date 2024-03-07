mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

For reference: [https://ostechnix.com/a-beginners-guide-to-cron-jobs/](https://ostechnix.com/a-beginners-guide-to-cron-jobs/)

Here I'm using crontab to copy a file from OneDrive to the Hadoop edge node (so I can use the server resources for analysis of the file)

-   Open a bash terminal on your local computer
-   Enter `crontab -e`
	-   It will open a Vim editor.
-   Hit `i` to enter insert mode
-   Simply add a crontab line!
	-   Format:
		-   {run cadence} {command}
	-   For example, add the following line:
		-   `0 22 * * * scp -i ~/.ssh/id_rsa ~/OneDrive\ -\ CVS\ Health/TODO.xlsx a522860@xhadrevrm7p:~/TODO/TODO.xlsx`
		-   This will copy the TODO file from OneDrive to the target folder on the edge node, once per day at 10pm.
-   Hit `esc` to exit insert mode
-   Press `:`
-   Enter `wq` (for write-quit) and press enter**