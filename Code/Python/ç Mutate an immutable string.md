# ç Mutate an immutable string
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***

## Problem

![Mutate%20a0aeffe06b914292a205b460244a7b95/Untitled.png](Media/Untitled%206.png)

![Mutate%20a0aeffe06b914292a205b460244a7b95/Untitled%201.png](Untitled%201%202.png)

## Solution

```python
def mutate_string(string, position, character):
    string = string[:position] + character + string[position+1:]
    return string

if __name__ == '__main__':
    s = input()
    i, c = input().split()
    s_new = mutate_string(s, int(i), c)
    print(s_new)
```