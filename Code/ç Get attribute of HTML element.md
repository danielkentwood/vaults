# ç Get attribute of HTML element

##### Metadata
created:: 2023-04-28 13:47
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[JavaScript]]
platform::
***

Let's pretend you have a div with `id = collections`

You can use javascript to retrieve attributes of that div. For example, let's say I want to get the width and height:

```javascript
const width = document.getElementById("collections").clientWidth;
const height = document.getElementById("collections").clientHeight;
```

You can also retrieve attributes by class. Let's say the div has `class = border`

```javascript
const elements = document.getElementsByClassName("border")
```
