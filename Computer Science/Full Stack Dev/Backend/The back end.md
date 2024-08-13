- what are examples of unstructured data?
	- content inside of emails or books or images
- for review on SQL see [[SQL]]
a. Action "statement" b. tableName c. conditions "clauses"

##### What happens when you make an http request
###### Review: http request
- Hyper text transfer protocol is the convention for request and serving data to client side applications
- when you type an address or url (universal resource locator) you command your browser to open a TCP (Transmission Control Protocol)
	
- The TCP channel finds the server that hosts the site you are attempting to reach. it starts a connection
- once the connection is established, the client sends a get request to the server to retrieve the webpage. afterward, it will close the connection. 

what a request looks like: 
- the client requests internet Domain Name Server to return an Internet Protocol address 
	- using the http convention it will then open a connection to the server at the address
	- if it finds something, then the server might respond with a 200 ok
```markup
|00 (OK)|This is the standard response for successful HTTP requests.|
|201 (CREATED)|This is the standard response for an HTTP request that resulted in an item being successfully created.|
|204 (NO CONTENT)|This is the standard response for successful HTTP requests, where nothing is being returned in the response body.|
|400 (BAD REQUEST)|The request cannot be processed because of bad request syntax, excessive size, or another client error.|
|403 (FORBIDDEN)|The client does not have permission to access this resource.|
|404 (NOT FOUND)|The resource could not be found at this time. It is possible it was deleted, or does not exist yet.|
|500 (INTERNAL SERVER ERROR)|The generic answer for an unexpected failure if there is no more specific information available.|
```
##### what is routing?
- the pair of uniform resource indentifier and an http verb (get, post, put, delete) is called a route
- matching these two based on a request is called routing
##### what is web api?
- clearly defined method of communication, an interface created by the back end 

###### what is middle ware?
- code that runs on the server between the request and the response back to the client
### Introduction to frameworks
- basically the main idea is in efforts of not reinventing the wheel when it comes to web development: 
	- many sites have overlapping features such as authentication, form validation, routing, connections with databases with code that can be reused instead of having to rewrite it every single time 
- It also gives developers standards in how to structure their code base that leads to greater uniformity and organization when working on a team. 
##### user interface frameworks
- bootstrap
- materialize
- semantic UI
- grommet
##### Frontend frameworks
- vue
- angular
- react
- ember
##### Back end frameworks
- spring mvc - java - ew
- Django - python - more opinionated, alot of features out of the box
- Flask - python - less opinonated than django
- ruby on rails - ew
- express - JS - very lightweight, very fast, very customizable

##### Web servers
- apache
- nginx