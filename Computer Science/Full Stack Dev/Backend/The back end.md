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
- react- ember
##### Back end frameworks
- spring mvc - java  ew
- Django - python - more opinionated, alot of features out of the box
- Flask - python - less opinonated than django
- ruby on rails - ew
- express - JS - very lightweight, very fast, very customizable

##### Web servers
- apache
- nginx

##### What is an Object-Relational Mapper (ORM)?
- it essentially an abstraction layer between a webframe work (or should I say that many webframe works provide one) that abstracts away the operations and querys of put, get, post, delete
- benefits of ORM:
	- it can be safer to abstract away queries to avoid malicious intrusions and hacking of queries

### Introduction: what is Node.js?

#### Parking lot: 
- what is really under the hood of nodejs and how is it any different from what we can do with a web bundler like vite?
	- what is the point of something like node js when you have something like vite, or is vite made with node and you can build your own run time? or is it like what the browser does which is run all the necessary outside scripts that allow applications to be asynchronous 

##### what is node?
- at its most basic level, node allows you to bring javascript code out of browser land. it allows code to run and accomplish anything that serverside languages such as ruby, php, c# and python can do. 
	- some of the additional things it can do that it cannot do on a browers: 
		- abiltiy to read and write to local files
		- create http connections
		- listen to network requests
###### Event driven
- Event driven by asynchronous events such as network requests, databasequeries, etc
- kind of how you might have an event listener and a sequence of code that occurs from that event being triggered
	- you might have two function bundles such as : 
		- reading from a file and then printing out the contents of that file
		- query database and then filter the results
	- the first thing might still be working but node will immediately being working on the second one which is query the database
###### nodejs and callbacks
 - these events rely on the use of callbacks. callbacks are essential to node
 - review on callbacks: 
	 - functions in javascript are first class citizens and as such can be assigned to varaibles or passed as argument to antoher function
- example:
```js
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end('Hello World!');
}).listen(8080);
```
- here we have these callbacks that are meant to run in the event of a request coming through
##### Dynamic and Static sites
 - static sites are generic information sites with css, images, html and js that wont change and the request fetches the files and the files are sent back. 
	 - static resources are those things like js, css, and images that will not change. that is the same process for fetching as static sites
- Dynamic sites will generate an html template with static resources that it will use. 
	- however when there are requests for dynamic information such as account information or search engine queries, then the request is instead forwarded to a web application that will process the request and make the necessary daatabase queries to send the data to the webserver along with the static resources like the html template in order to send back the completed site. 
	- the use of reusable code, templating, dynamic component and data generation is an example of dynamic sites, i.e using react especially with react-router
###### Client server overview and Dyanmic requests
- *essential question*: what happens when a server receives a dynamic request from a browser. 
	- what operations need to be performed by server-side code?
 **What can be included in a Request?**
- Method that defines the required action: `GET, POST, HEAD, PUT, DELETE`
	- HEAD gets metadata from a specific resource that can be used for example to see whether the resource was updated and can then do a more costly GET request
- URL parameters: `http://example.com?name=Fred&age=11` takes key:value pairs
	- ? always separates the rest of the URL from the parameters
	- = is the separater between a key and a value
	- & is the separating anothey key:value pair in the url parameters
		- because of the nature of being able to change the url parameters in the url bar, requests that change data on the server are not allowed through url parameters and get requests
- POST data  that will be added as data to the server
- Client side cookies - can include keys that is information about the client for authorization purposes on a site

- webservers will then process the request and respond with 200 ok if it was found, 404 if not found or 403 which means forbidden (i.e they dont have authorization bc they're not logged in)
- both static and dymanic websites use the same communication protocol or patterns

**POST**
- when you post you get the 302 FOUND indicating that a post was successful 
- site to sniff website requests : https://websniffer.com/

#### Getting started with Node.js
##### modules
- node comes pre packaged with modules that can be used right out of the box.  for a complete list: https://www.w3schools.com/nodejs/ref_modules.asp
##### HTTP Module
- the most essential part in creating a server is the http module that handles requests. 
- on a local machine you can go to your browser and put `http://localhost:8080` or whatever number you used to listen for
- to get set up, see: 
```js
import http from "http";

http.createServer(function (req, res) {
	res.write(200, {'Content-Type': 'text/html'});
	res.end("Hello world!");
}).listen(8080);
```
- notice that the create server method requires a callback function that accepts a request  and resolution parameter. 
- you then use the req and res parameters to define what behaviors will happen when a request comes through
	- again: a request is made by actually attempting to visit your page after using `node <filename>` . it will literally create a local server
###### http and url
- you can access parts of the url from the request and use in the code: 
```js
var http = require('http');  
var url = require('url');  
  
http.createServer(function (req, res) {  
  res.writeHead(200, {'Content-Type': 'text/html'});  
  var q = url.parse(req.url, true).query;  var txt = q.year + " " + q.month;  
  res.end(txt);  
}).listen(8080);
```
- notice here the url imported and how the url object uses a method called parse that will accept the request url from the req argument parameter
##### File system
- useful node documents on the file stream: https://nodejs.org/en/learn/manipulating-files/writing-files-with-nodejs
 - one thing to note about he fs is that by default, they are asynchronous operations that will be non blocking. if you want it to be blocking i.e if you are working in a try/catch block for error handling you can append Sync to the end of the function call to block it and hence the try block will not close out until the fs has finished its process
- getting started: 
```js
import http from 'http';
import fs from 'fs';

http.createServer(function (req, res) {
  //Open a file on the server and return its content:
  fs.readFile('demofile1.html', function(err, data) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    return res.end();
  });
}).listen(8080);
```
- notice here the presence of the http server once again. seems that all good things happen first with the presence of the http server. 
- notice here that inside the createServer callback function we 
##### URL Class
- over all the url module breaks up a web address into readable parts. 
- if a passed url is not recognized, then you can pass an error and present the 404 error text
```js
import http from 'http';
import url from 'url'; 
import fs from 'fs';

http.createServer(function (req, res) {
  const q = url.parse(req.url, true);
  const filename = "." + q.pathname;
  fs.readFile(filename, function(err, data) {
    if(err) {
      res.writeHead(404, {'Content-Type': 'text/html'});
      return res.end("404 Not Found");
    }
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    return res.end();
  });
}).listen(8080);
```
- something to note here is the presence of the `url.parse()` that takes the passed req request and extracts the pathname. 
- then passed on a parameter passed in the path name i.e `localhost:808/summer.html` , it will read the file named 'summer.html' and serve that. 

##### Events
- The events module allows us to replicate on the backend a way to handle user events such as keyboard pressed, mouse movements, mouse clicks, etc. 
- the events module along with the event emitter gives you control over what things to listen for and with the emitter, you can also control when those events get triggered
	- some examples of events are when you open a file or when you use the emitter to emit the event, for example: 
```js
var events = require('events');
var eventEmitter = new events.EventEmitter();

//Create an event handler:
var myEventHandler = function () {
  console.log('I hear a scream!');
}

//Assign the eventhandler to an event:
eventEmitter.on('scream', myEventHandler);

//Fire the 'scream' event:
eventEmitter.emit('scream');
```
- notice here that the emitter is passing a string that the .on() listens for . 
##### Visual on node and modules: 
https://www.youtube.com/watch?v=fBNz5xF-Kx4
- covers modules that go over OS info
- url
- event and event emitter
	- including useful logging of error information
- http server serving json as a restful api
	- handling css files as well
	- dynamic filepaths
	- getting the extensions of files
- another video series (12 videos) on node and express: https://www.youtube.com/watch?v=fBNz5xF-Kx4
	- includes topics on clients and servers
	- requests and responses
	- view engines, middleware
	- get, post, delete,
	- express router and mvc
##### file uploads and emails
 - uploads: https://www.w3schools.com/nodejs/nodejs_uploadfiles.asp
 - emails: 
#### Debugging Nodejs in Chrome
- for the time being debuggin in lvim is absolutely fucked 
- in chrome: 
	- visit `chrome://inspect`
	- make sure these configurations are present: 
		- 127.0.0.1:9229 (under discover network targets)
	 - in your node file in the terminal, run `node --inspect-brk filename.js`
	- click 'open dedicatd Devtools for node'
	- it will automatically halt execution, set a breakpoint and go to town!

### Environment Variables
What are environment variables?:
- variables that have environment specific values such as information on your machine that can be used to modify conditions based on the specific environment that the code base is running on. 
	- This end is supposed to result in not having to change the code base but being able to have different conditions be meant if for example we're running on a production environment versus a devleopment environment
- They are also used for hiding credentials, database urls, or api keys
#### Loading environment variables
1. pass it as an argument when you run the script with node 
	- `NODE_ENV=prod VIDEO_URL="https://www.youtube.com/watch?v=X2CYWg9-2N0" node index.js
	- problem with this method is if you have this command defined in an npm script in your package.json you will have important possible sensitive information visible on that repo
2. export environment variables using the shell command export to save the variables for the current shell session only 
	- `export NODE_ENV=prod VIDEO_URL="https://www.youtube.com/watch?v=X2CYWg9-2N0"`
3. dotenv - one of the most common ways to load environment variables. 
	- . you need to install the npm package and create a file called .env in the root of your project that will have all the environment variables with the `NAME="VALUE"` 
	- create a `.gitignore` file and place the .env file so it doesnt get tracked by the repo
	- finally import as soon as possible into your app `require("dotenv").config();`
	- running node filename.js will work importing the enviroment variables
#### accessing environment variables
use `process.env.NODE_ENV === "prod" ? <stuff> : <other stuff>`
- *note* - environment variables are always strings so you will need to convert other primitive types into a string
- documentation on dotenv: https://www.npmjs.com/package/dotenv#-documentation

## EXPRESS
### Intro to express
What is express?
- express is a backend frame work for nodejs. while I have use node on its own to set up servers, it can be verbose and as the complexity of the site increases, so will the complexity and verbosity of writing everything yourself. Express is a framework that helps with handling the complexity and gives some flexibility in how things are done and is known to be unopinionated
##### Getting started with an express server
```js
import express from 'express';
// dont forget to include "type": "moduel", in package.json
const app = express();

app.get("/", (req, res) => res.send("Hello, world!"));

const PORT = 3000;
app.listen(PORT, () => console.log(`My first Express app - listening on port ${PORT}!`));
```
- here we have the express server being told to respond to get requests to a route "/" with the text hello world
- then the express app is being told to listen for port name in this case 3000. which  i guess is the default address
	- one thing to note is that normally you use env variables for the port name and then you go something like this: `const PORT = process.env.PORT_VAR || 3000;` 
		- meaning to use the environment variable or else 3000 as the standard one. 
###### Middleware
- middle ware are functions that happen before express server responds to the get request. the request will get added to an object of requests by the server and then it will get passed through these middle ware functions. 
	- not sure of the purpose of them outside of telling express to eventually respond to the get request
###### Auto-restart your server on changes
- instead of having to run node app.js every change, you can run `node --watch app.js` and node will listen for changes and auto restart your server for you.

###### Implementing basic site with dynamic html serving
```js
import express from 'express';
import path from 'path';
import { fileURLToPath } from 'url';

const app = express();

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
app.get('/', function(req, res) {
  const filepath = path.join(__dirname, "index.html");

  res.sendFile(filepath, function(err) {
    if(err){
      res.status(500, "something went wrong with the server!");
      return;
    }
  })

})
// i struggled to get /:name to match with index, perhaps '*' would have matched with anything and could have processed the paramstring easier
app.get('/:name', function(req, res) {
  const params = req.params.name;
  let fileName = "";
  console.log(params);

  switch (params) {
    case "":
      fileName = "index.html";
      break;
    case "about":
      fileName = "about.html";
      break;
    case "contact-me":
      fileName = "contact-me";
      break;
    default:
      fileName = "404.html";
  }

  const filepath = path.join(__dirname, fileName);
  console.log("filepath is" + filepath);

  res.sendFile(filepath, function(err) {
    if (err) {
      res.status(500).send("There was a server error: 500");
      return;
    }
    console.log("sent file");
  });
});

const PORT = 3000;
app.listen(PORT, () => console.log(`you are listening on port ${PORT}`));

```
- one thing to note here is that this is actually more code than when I just used nodejs as server without the framework but I think this will be simplified as I learn more about it. 
	- this was actually a second iteration where I was able to take dynamic parameter values from url and use switch block to dynamically send the html file to populate
		- I was not however able to handle the index '/' with a single app.get() like Iwas able to do with just node.js. perhaps this is the cost of moving with a framework when all you have is a static website
	- update: I could have used `"/(:name)"` that would either match with "/" or some thing else that is a dynamically accessed parameter

### Routes
routes allow us to match a requests http verb (get or post) and URL path to the appropriate middleware functions. 

##### anatomy of a route
```js
app.get("/", (req, res) => res.send("Hello, world!"));
```
- this gets us a match only with get requests that have '/' as the sole parameter in the url
- you also have `app.post()` that has matchers same as get
- there is also app.all() that would matcher with all http verbs (get, post, put, delete, etc)
- order matters because if you have a app.get(`"*"`) and after app.get('/messages') the second route will never be reached even if you have /messages as exact parameter because it iwll first match with the wildcard match
- you would need to reverse the order in which they are declared and defined in order to bring out the intended behavior 
###### route parameters
- as seen above, you can access route or url parameters by putting a : followed by the name of the parameter
```javascript
app.get("/:username/messages", (req, res) => {
  console.log(req.params);
  res.end();
});

//GET /odin/messages will return this {username: 'odin'}
```
- as you can see, it returns an objec that you have to use dot notation naming the key to the value
- you can place multiple parameters in the route and it will extract it to the same object
###### query parameters
- query parameters are a part of the URL that appears at the end and is denoted by a **?** to start the beginning of the query parameter
	- follows the format of key=value
	- each & denotes another key=value pair
- unique because its actually not part of the path itself but more of arguments that can be passed
- express will automatically process these queries into a req.query object. if there are repeat keys, it will put all those values into an array
```js
/**
 * GET /odin/messages?sort=date&direction=ascending will log
 * Params: { username: "odin" }
 * Query: { sort: "date", direction: "ascending" }
 *
 * GET /odin/messages?sort=date&sort=likes&direction=ascending will log
 * Params: { username: "odin" }
 * Query: { sort: ["date", "likes"], direction: "ascending" }
 */
app.get("/:username/messages", (req, res) => {
  console.log("Params:", req.params);
  console.log("Query:", req.query);
  res.end();
});
```
- you can see here the difference in accessing the params or the query of the url

#### Routers
consider a longer url such as `POST /books/:bookId/reserve` and you have something different for authors and specific author pages. the main app page can start to get long, for organization we can group routers by function or destination and have their respective routes and param logic for their category
```js
// app.js
const express = require("express");
const app = express();
const booksRouter = require("routes/booksRouter");
const authorsRouter = require("routes/authorsRouter");
const indexRouter = require("routes/indexRouter");

app.use("/books", booksRouter);
app.use("/authors", authorsRouter);
app.use("/", indexRouter);

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`My first Express app - listening on port ${PORT}!`);
});
```
- notice here importing routers for books and other logical router groupings
- also notice how the main express server is specifying how the path will be directed to respective router with app.use()
- what is app.use() for?
	- its used to specify middleware as the callback function instead of a specific response. 
```js
// routes/authorsRouter.js
const { Router } = require("express");

const authorsRouter = Router();

authorsRouter.get("/", (req, res) => res.send("All authors"));
authorsRouter.get("/:authorId", (req, res) => {
  const { authorId } = req.params;
  res.send(`Author ID: ${authorId}`);
});

module.exports = authorsRouter;
```
- here is an example implementation of what one of those routers would look like
- notice how only destructuring the Router object from express and you're using exports for the router
- also notice how the router.get("/") is relative path to within the /author path instead of the root "/" directory. in other words, the paths in routers extend the parent path
