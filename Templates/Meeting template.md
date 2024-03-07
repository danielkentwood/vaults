# <% tp.file.title %>
<% await tp.file.move("/Meetings/" + tp.file.title) -%>

##### Metadata
title:: <% tp.file.title %>
created:: <% tp.file.creation_date() %>
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/management
kind:: #meeting
status:: #status/raw
parent::
***
## Log


## Tasks

