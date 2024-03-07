# ç Array intersection and difference in Javascript

##### Metadata
created:: 2023-03-04 01:17
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[JavaScript]]
platform::
***


```javascript

// intersection = keep only the elements that are common between a and b
let intersection = arr1.filter(x => arr2.includes(x));

// difference = keep elements from a, but exclude the intersection between a and b
let difference = arr1.filter(x => !arr2.includes(x));

// symmetric difference = keep all elements from a and b, except for the intersection between them
let symmetric_difference = arr1
                 .filter(x => !arr2.includes(x))
                 .concat(arr2.filter(x => !arr1.includes(x)));      
```

Original source is stack overflow: https://stackoverflow.com/questions/1187518/how-to-get-the-difference-between-two-arrays-in-javascript?page=1&tab=scoredesc#tab-top