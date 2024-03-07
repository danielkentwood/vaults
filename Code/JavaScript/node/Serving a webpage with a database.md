# Serving a webpage with a database
created:: 2022-07-19 15:30
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #zettel 
status:: #status/seed
parent:: [[back-end development]]
***


## Set up the server and serve a website with Node:
* [[Node.js]] is a [[JavaScript]] back-end runtime environment that lets developers run async server-side scripts to produce dynamic content prior to the browser. 
* YouTube video: [Server-side with Node.js](https://www.youtube.com/watch?v=wxbQP1LMZsw&list=PLRqwX-V7Uu6YxDKpFzf_2D84p0cyk4T7X&index=9)

## Databases
### MongoDB
* [[MongoDB]] is a [[NoSQL]] DB. Instead of tables, it stores data in [[JSON]]-like documents. 
* https://www.w3schools.com/nodejs/nodejs_mongodb.asp
* https://www.geeksforgeeks.org/mongodb-tutorial/?ref=gcse
* stores records as [[BSON]] documents (binary representation of JSON, making I/O very efficient and rapid). Here's more info on documents: https://www.mongodb.com/docs/manual/core/document/#:~:text=Document%20Size%20Limit,MongoDB%20provides%20the%20GridFS%20API.

### neDB (subset of MongoDB API; no longer maintained)
* YouTube video: [Getting started with NeDB](https://youtu.be/xVYa20DCUv0)
* YouTube video: [Querying neDB database](https://youtu.be/q-lUgFxwjEM)

