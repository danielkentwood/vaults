---
title: <% tp.file.title %>
mode: "#mode/gnosis"
kind: "#annotation"
annotation-target: 
created: <% tp.file.creation_date() %>
last modified: <%+ tp.file.last_modified_date() %>
<% await tp.file.move("/Media/Annotations/" + tp.file.title) -%>
---

