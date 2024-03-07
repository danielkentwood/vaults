# ç sWAP cASE in Python
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***


## Problem

![[Media/Untitled 6.png]]

## Solution

```python
def swap_case(s):
    new_s = ''
    for l in s:
        if l.isalpha():
            if l.isupper():
                new_s = new_s + l.lower()
            elif l.islower():
                new_s = new_s + l.upper()
        else: 
            new_s = new_s + l
    return new_s

if __name__ == '__main__':
    s = input()
    result = swap_case(s)
    print(result)
```

Built-in function solution

```python
def swap_case(s):
    return s.swapcase()

if __name__ == '__main__':
    s = input()
    result = swap_case(s)
    print(result)
```