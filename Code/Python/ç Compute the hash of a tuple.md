# ç Compute the hash of a tuple
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***


## Problem

![Tuples%202c98f2f5b4c141cba68593a58c883e3b/Untitled.png](Untitled%2012.png)

## Solution

```python
if __name__ == '__main__':
    n = int(input())
    integer_list = map(int, input().split())
    print(hash(tuple(integer_list)))
```