# ç Apply user-supplied list of list operations to a list
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***

## Problem

![List%20functions%20b3eaee37a10b4c3f9b4b30f788742f4e/Untitled.png](Media/Untitled%204.png)

![List%20functions%20b3eaee37a10b4c3f9b4b30f788742f4e/Untitled%201.png](Untitled%201%201.png)

## Solution

```python
if __name__ == '__main__':
    N = int(input())
    my_list = []
    for _ in range(N):
        new_line = input().split()
        command = new_line[0]
        if command in 'insert':
            my_list.insert(int(new_line[1]),int(new_line[2]))
        elif command in 'print':
            print(my_list)
        elif command in 'remove':
            my_list.remove(int(new_line[1]))
        elif command in 'append':
            my_list.append(int(new_line[1]))
        elif command in 'sort':
            my_list.sort()
        elif command in 'pop':
            my_list.pop()
        elif command in 'reverse':
            my_list.reverse()
```