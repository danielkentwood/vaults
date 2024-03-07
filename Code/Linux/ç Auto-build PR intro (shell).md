# ç Auto-build PR intro (shell)
created:: 2022-11-11 17:30
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform::
***

This shell script builds the skeleton for the intro comment of a pull request. For the "detailed list of changes" section, it grabs the [[git diff]] (files only) between master and HEAD of the current branch, and formats them into a bullet list. 

```bash
#!/bin/bash

echo """
# Summary of changes

# Context and motivation

# Detailed list of changes
"""

for p in $(git diff --name-only master HEAD)
do
	echo "* \`$p\`:"
	echo " *"
done

echo """

# Validation of changes
"""
```

