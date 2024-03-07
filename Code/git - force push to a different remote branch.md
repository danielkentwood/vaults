# git - force push to a different remote branch

##### Metadata
created:: 2024-02-14 15:08
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[git]]
***

See this stack overflow: https://stackoverflow.com/questions/36927956/how-to-do-a-forced-push-to-another-branch-in-git

```
git push origin --force localBranchName:remoteBranchName
```