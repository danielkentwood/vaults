# ç Nested Lists
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform:: [[HackerRank]]
***


## **Problem:**

![Nested%20Lists%2007ac064300854fc3ab896f3ae0631c99/Untitled.png](Untitled%207.png)

![Nested%20Lists%2007ac064300854fc3ab896f3ae0631c99/Untitled%201.png](Untitled%201%203.png)

## Answer:

```python
if __name__ == '__main__':
    class_l = []
    for _ in range(int(input())):
        name = input()
        score = float(input())
        class_l.append([name,score])
    names = sorted([i for i,j in class_l 
                    if j==sorted(list(set([j for i,j 
                                           in class_l])))[1]])
    for i in names:
        print(i)
```