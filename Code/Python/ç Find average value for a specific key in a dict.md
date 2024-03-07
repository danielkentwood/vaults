# ç Find average value for a specific key in a dict
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***

## Problem

![Finding%20the%20Percentage%2054801338a2074282a2389d90af5c79a0/Untitled.png](Media/Untitled%203.png)

## Solution

```python
if __name__ == '__main__':
    n = int(input())
    student_marks = {}
    for _ in range(n):
        name, *line = input().split()
        scores = list(map(float, line))
        student_marks[name] = scores
    query_name = input()
    marks = student_marks[query_name]
    print('{:.2f}'.format(sum(marks)/len(marks)))
```