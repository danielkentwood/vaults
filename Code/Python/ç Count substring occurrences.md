# ç Count substring occurrences
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***


## Problem

![Find%20a%20string%20916c4a7b8489408588c85a93a34db7ac/Untitled.png](Media/Untitled%201.png)

## Solution

My solution

```python
def count_substring(string, sub_string):
    counter = 0
    for i in range(0,len(string)-len(sub_string)+1):
        if string[i:i+len(sub_string)] in sub_string:
            counter+=1
    return counter

if __name__ == '__main__':
    string = input().strip()
    sub_string = input().strip()
    
    count = count_substring(string, sub_string)
    print(count)
```

Using the .startswith() method

```python
def count_substring(string, sub_string):
    count = 0
    for i in range(len(string)):
        if string[i:].startswith(sub_string):
            count += 1
    return count
```