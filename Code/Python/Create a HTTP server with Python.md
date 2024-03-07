# Create a HTTP server with Python
created:: 2022-05-13 13:36
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
platform::
***

## Resources

For prototyping/dev, you can create a quick local server with the python http library.

There is a CLI. You just have to supply the port. This example below will launch the server on port 8000.

`python -m http.server 8000`

Then you can open localhost:8000 in your browser and navigate to the file(s) you're developing. 

If you serve to a port on an internal server, anyone on that server can visit that port and view what is on it. 

