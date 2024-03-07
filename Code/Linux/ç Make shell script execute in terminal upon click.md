# ç Make shell script execute in terminal upon click
created:: 2022-11-11 09:38
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform::
***

If you want to be able to just click on a shell script and have it execute in the terminal, you need to:
1. Write the shell script
2. Save it as `<filename>.command` instead of `<filename>.sh`
3. Give executable permissions with `chmod 777 <filename>.command`