
# ç parameter substitution in Bash
title:: ç parameter substitution in Bash
created:: 2022-05-09 14:12
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
***


## Remove characters
To remove characters _starting with and after_ a specified pattern, you can use the `%` symbol to indicate that ensuing string is the pattern to start with. It will look for the last occurrence of that pattern. 

#### Remove all characters after last occurence of a pattern
In this example below, I want everything removed starting with the last space character. 

```bash
TST="Find a string 916c4a7b8489408588c85a93a34db7ac";
echo "${TST% *}"
```

Result: `Find a string`



#### For all files in a directory, remove all chars after last occurence of a pattern
For each file name in the current directory, remove all characters starting with the last space character.

```bash
for p in ./*.md
do
	mv "$p" "${p% *}.md"
done
```

If you want to do this recursively, the first line should be:

	for p in ./**/*.md


#### For all files in a directory, remove a pattern from the beginning of a file
In this example, I'm removing the pattern "" from the beginning of each file that contains it.

```bash
for p in ./Ω*.md; do mv "$p" "${p///}"; done;
```



## Add characters
#### Add a character at the beginning of each file in a directory
Let's suppose I want to add the string "" to the beginning of every markdown file name in the current directory:

```bash
for p in ./*.md
do 
	mv "$p" "./${p#./}"
done
```

Note that we are using the `#` symbol to remove all characters prior to and including the pattern specified after it. In this case, the file path includes the `"./"` substring, so we want to (1) remove that, and (2) replace it with `"./"`.



## Resources
* [https://www.cyberciti.biz/tips/bash-shell-parameter-substitution-2.html](https://www.cyberciti.biz/tips/bash-shell-parameter-substitution-2.html)
