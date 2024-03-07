# Linux sed
title:: Linux sed
created:: 2022-05-09 14:12
modified:: <%+ tp.file.last_modified_date() %>
mode: #praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
***

The `sed` command lets you perform string replacement.

The syntax is:

```bash
sed -i 's/string_to_be_replaced/new_string/g' *.*
```

- The -i option lets you edit the source file directly.
-   the s flag at the beginning of the string specifies that this is a 'substitution' command
-   the g flag at the end of the string specifies that this replaces all instances of the string globally.

#### Example
Look through all sql files in a directory and replace every instance of "PROJECT: Maternity Engine, Gestational Diabetes" with "PROJECT: Gestational Diabetes Management NBA"

```bash
sed -i 's/PROJECT: Maternity Engine, Gestational Diabetes/PROJECT: Gestational Diabetes Management NBA/g' *.sql
```
  

> [!Important]
> On OSX, the `-i` flag takes an argument specifying a backup suffix. To suppress the backup you have to provide an empty string. For example, `sed -i '' 's/pattern/replacement/g *.*'`


## Resources
* [https://www.linuxteck.com/sed-commands-in-linux/](https://www.linuxteck.com/sed-commands-in-linux/)

