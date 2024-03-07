# ç String Split and Join
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***

## Problem

![String%20Split%20and%20Join%2019c5027943634adba9d623ebde119f7c/Untitled.png](Untitled%209.png)

## Solution

```python
def split_and_join(line):
    return "-".join(line.split(" "))

if __name__ == '__main__':
    line = input()
    result = split_and_join(line)
    print(result)
```