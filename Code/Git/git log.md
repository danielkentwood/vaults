# Git log

##### Metadata
created:: 2023-02-24 11:10
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[git]]
platform::
***

Show the log, but with just the commit hash, who did the commit, when it happened, and the short description:
```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Output:
```
ac066fa - Daniel Wood, 16 hours ago : minor changes to cohort nb
f10f722 - Daniel Wood, 17 hours ago : update gitignore
b4dece2 - Daniel Wood, 8 days ago : refactoring out recommendation
1fc0f74 - Daniel Wood, 8 days ago : Merge branch 'master' of github.aetna.com:analytics-org/dementia-NBA into v2_mbr_cohort_MMT_JSON
0aa72dc - Wood, Daniel K, 2 weeks ago : Merge pull request #17 from analytics-org/v2_member_attributes
d0ca312 - Wood, Daniel K, 2 weeks ago : Merge branch 'master' into v2_member_attributes
ced6257 - Wood, Daniel K, 2 weeks ago : Merge pull request #8 from analytics-org/ccp-conversions
```

