# ç recursively list all SQL tables used in directory

##### Metadata
created:: 2023-11-08 11:56
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform::
***

Here is a bash command to recursively search for and list all SQL tables that are used in SQL (or HQL) files in a directory. It also prints the file path for each hit. 

```bash
grep -r --include=\*.sql --include=\*.hql -E -o -i '(FROM|JOIN)\s+[a-zA-Z0-9_]+\.[a-zA-Z0-9_]+' . | sed -E 's/(FROM|JOIN)\s+//i' | sort | uniq
```


- `grep -r --include=\*.sql --include=\*.hql -E -o -i`: This command uses `grep` to search the directory. The `-r` flag ensures that the search is recursive. The `--include` parameter lets you pass a filetype to limit the search space. The `-E` flag enables extended regular expression syntax, `-o` prints only the matched parts of matching lines, and `-i` makes the search case-insensitive. 
- `'(FROM|JOIN)\s+[a-zA-Z0-9_]+\.[a-zA-Z0-9_]+'`: This regular expression pattern is part of the above grep function. It matches any line that contains `FROM` or `JOIN` followed by (one or more alphanumeric characters, or underscores), a period, and again (one or more alphanumeric characters, or underscores). 
- ` . `: This is the final argument for the grep function. It specifies where to start the search from, and in this case it is specifying the current working directory.
- `sed -E 's/(FROM|JOIN)\s+//i'`: This command uses the `sed` stream editor to remove the `FROM` or `JOIN` and any following whitespace from each line. The `-E` flag enables extended regular expression syntax, and the `i` flag makes the substitution case-insensitive.
- `sort`: This command sorts the lines in ascending order.
- `uniq`: This command removes duplicate lines.

