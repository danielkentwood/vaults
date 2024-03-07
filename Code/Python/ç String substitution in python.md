# ç String substitution in python
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***

## Problem

![What's%20Your%20Name%201149b09da3b74fc5882189aae0176ede/Untitled.png](Untitled%2015.png)

## Solution

```python
def print_full_name(a, b):
    print("Hello {0} {1}! You just delved into python.".format(a,b))

if __name__ == '__main__':
    first_name = input()
    last_name = input()
    print_full_name(first_name, last_name)
```