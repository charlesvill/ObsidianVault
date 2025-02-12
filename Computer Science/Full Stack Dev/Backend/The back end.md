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
- code that runs on the server between the request and the re to the client
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

##### Loading assets into express app
```js
const path = require("path");

const assetsPath = path.join(__dirname, "public");
app.use(express.static(assetsPath));
```
- include this in your main app.js express app. make sure that you have the path object imported 
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

### Controllers
- known as a middle man that is the brains of the operation that delegates to other systems what to do. 
	- it is really a function with really well-defined responsibilities as part of the MVC pattern
	- it sits between the view and the model that references both in its files and calls functions in both to either request updates or fetch data from the model or calling a function passsing the updated data to the view. 
	- The controller also might handle the input validation that will later be seen to sanitize user input
- What is the MVC pattern?
	- Model - View - Controller : a design pattern for web applications where the model is the data logic inthe back end that handles storing and quering data as well as applying logic, algorithms etc. the View is the user interface that displays the data processed by the model and the controller is the middle man between the backend and the frontend that handles how user interactions are routed and what data gets passed to the backend Model to process or store. 
- what is the difference in responsibilities in something like a router vs a controller?
	- the Router handles what path will be accepted as well as what controller it will hand it off to
	- the Controller is a seperate file that is the logic of what happens with the data. it will handle requesting from the model a query, reshaping the data, and sending the response to the view 
	- a router more or less is a controller  but there is value in specifiying them as being different or specific tasks within the function of a controller enough to warrant its own separate directory folder path
- rough flow of responsibilites: with a query of `https://domainname/users`
	- Request arrives at app to (/)
	- app middleware handles any app wide processing like authentication etc.
	- Router will match with /users and hands off to the router 
	- Router will call any middle ware it needs for that scope/instance such as authentication, error checking and then hand off to a specific controller to handle the response logic
	- controller applies business logic and closes response cycle with either 200 success and data or error codes
##### Principles of MVC
- when thinking about if your application logic is being faithful to the MVC pattern, consider the principle values behind following an MVC pattern: 
	- Easy to maintain - 
		- when you need to fix something, you know based on what it is you need to fix where to look because the project file directory files are organized by their purpose in the application. 
		- Fixing one component does not involve having to fix or refactor a bunch of other code that is not involved in the direct fix
	- Easy to scale - 
		- because of the seperation of purposes, it is easier to think separately about your application and "chunk" a task or functionality that needs to expand without having to consider a larger context of logic that is intertwinded with the part that needs scaling. 
		- expanding on the previous point - its easier to think of a focus component in a vacuum, or isolated and focus on its contribution or goal for scaling and not so much on other components that are interacting with it. 
	- Easy to Understand- 
		- because of the separation of concerns it should be easier to understand what each component does
#### Handling responses
- example of methods you might use in controllers: 
	- `res.send()` - this is flexible and will set the `Content-Type` header based onthe data you pass it
	- `res.json()`- more explicit form of  responding to request
		- The use case for this is it will automatically convert non-object values to json while res.send will not. 
	- `res.redirect()` allows for redirecting client to diffferent URL
	- `res.render()` - used with template engine it will send rendered html template
	- `res.status()` - useful for setting the status code manually 
		- note that you must do the status before the send. the status will not end the response to the request. 
- one thing to  note is that a function that has res.send() will not exit the function only terminate the request. 
```js
app.use((req, res) => {
  // This works and this ends the request-response cycle
  res.send("Hello");

  // However, it does not exit the function so this will still run
  console.log('will still run!!');

  // This will then throw an error that you cannot send again after sending to the client already
  res.send("Bye");
});
```
- this is example of the above statement
#### Middleware
a core concept in express and play important role in handling requests and responses. 
- they sit between the incoming request and the final intended route handler
**parking lot**:
- how does middleware fit in context with MVC pattern? 
	- it falls under the umbrella of controller that might call the model to request data, and eventually sends a response 
- in practical terms, what is the difference between req.use() and router.use()/router.get()
	- essentially same methods in different instances/scoping 
##### anatomy of middle ware function
- typically has three arguments though there are some with four:
	- `req` - the request object, which represents the incoming http request
	- `res` - the response object, which represents the http response that will be sent back
	- `next` - the function that pass the control to the next middleware function in the chain (optional)
			- important to note that the naming is purely conventional and really could be named naything
- the purpose of a middleware function: 
	- modify the request for a specific package (res.render will need setting of res.locals)
	- executing additional code (for validation of forms or authentication)
	- calling next middle ware function in theh chain
	- ending the request-response cycle ( no more middle ware functions even if there are some placed after the ending)
###### application-level middleware
- bound to instance of Express using `app.use()` as opposed to a router level middleware that is bound to instance of express router usig `router.use()`
- similar functions like app.get()/use/post/etc
- typically they are placed at the top level to ensure that they run first.
	- these middleware functions will not run if the req/resp cylcle is ended before the middle ware function runs.
- if you do not specify a path, it defaults to `/` and will match every single incoming request
	- common middle ware functions are: 
		- express.json, express.urlencoded - body parsers that allow to parse incoming request body to use through re.body
		- serving static files( app.use(express.static('public))) serving static files such as html, css, js, images. you can pass arguemnt to specify which directoyr to serve the static file
###### router-level middleware
- simliar to app-level middleware but is bound to instance of express router using `router.use`
	- when you use routers, you'll destructure the express obj for the router `const {router} = express();` 
- this will match only when the request matches the specific route 

###### basic middleware function
```js
function myMiddleware(req, res, next) {
  // Perform some operations
  console.log("Middleware function called");

  // Modify the request object
  req.customProperty = "Hello from myMiddleware";

  // Call the next middleware/route handler
  next();
}
app.use(myMiddleware);
```
- here by using app.use(myMiddleware)  registers this function as an application-level middleware
- you also gave a customProperty in the request that can be accessed by middleware functions following this function, called by next();
- notice the next() that is going to pass the control to the next middle ware function in the chain
	- *what is this chain? I need to see an example visual of what this chain can look like*
- important to note that middleware functions are executed int he order thaty they were defined or registered in the app, the sequence in which you define your middleware functions does infact matter. 
	- for example, some middlware functions that change the request object and those shoudl be ithe very top of your application so you can see theri changes in all the middle ware functions that follow it below it. 

##### Controllers
controllers are just functions that also classify as middleware that are used by route handlers
- controllers come into play when a requests hits a server and a router matches the requsted http verb and path.
- the route will determine which router will handle the requstbased on the defined middleware chain you set up. 
- from there, the controller takes over and takes the actgions needed to fulfill the request
	- this could involve pulling data from the model (app logic back end), processing data, updating model with new data etc. 
- once controller completes tasks, it will hand it off to the view to render the data in a suitable format for the client
	- can be html, or even json responses like the json responses received from apis interacted with
- naming conventions for controllers are usually based on the router they will be attached to (ie get route -> getsomething(), post -> createSomething, delete -> deleteSomething(), etc)
###### sample controller
```js
// user controller file - controllers/userController.js
import someDBQueryToGetUser from "db/queries";

const getUserById = async (req, res) => {
  const userId = req.params.id;

  const user = await someDBQueryToGetUser(userId);

  if (!user) {
    res.status(404).send("User not found");
    return;
  }

  res.send(`User found: ${user.name}`);
};
```
- you'd see this get used by passing request params with the id `router.get("/user/:id", getUserById)` queries the db for the user (notice that is async bc its searching file system) 
- if the user is not found then, notice the `res.status(404).send("user not found")` and the return after it because the other lines will keep running if you dont hit the return. sending response does not stop the function execution itself. 
- if its found then `res.send()` will by default send a 200 status 
##### Handling Errors
- quickest way to handle errors would be to wrap the async functionality in a try/catch block
- see this implementation of an express async error handler to see how spread operator and args works: https://github.com/Abazhenov/express-async-handler/blob/master/index.js
	- wrapping our async function in this will automatically handle wrapping our promise in try/catch and call next with the error in the event of an error
		- the name is `asyncHandler`  imported by `const asyncHandler = require("express-async-handler");`
###### Handling errors with a special middleware
```js
// Every thrown error in the application or the previous middleware function calling `next` with an error as an argument will eventually go to this middleware function
app.use((err, req, res, next) => {
  console.error(err);
  res.status(500).send(err);
});
```
- this is always put at the end of the chain of middleware functions to ensure that it is the very last middleware function so that it handles errors bubbling down from other middleware functions before it 
- one important thing to note is that this error handling middleware function requires four parameters and if one is excluded, it will not be recognized as an error middleware function. so all four will be needed even if you are not using all four. the error object must be the first one in the callback
```js
app.use((req, res, next) => {
  throw new Error("OH NO!");
  // or next(new Error("OH NO!"));
});

app.use((err, req, res, next) => {
  console.error(err);
  // You will see an OH NO! in the page, with a status code of 500 that can be seen in the network tab of the dev tools
  res.status(500).send(err.message);
});
```
- this will get triggered by middleware functions that throw errors and by previous mw fn that use the next `next(err)`
	- express can tell them apart by the `four parameters`
###### custom errors
- you can create custom errors by extending the errors class component (ew)
```js
class CustomNotFoundError extends Error {
  constructor(message) {
    super(message);
    this.statusCode = 404;
    // So the error is neat when stringified. NotFoundError: message instead of Error: message
    this.name = "NotFoundError";
  }
}
```
- then you call call it `throw new CustomNotFoundError("not found")`
```js
app.use((err, req, res, next) => {
  console.error(err);
  // We can now specify the `err.statusCode` that exists in our custom error class and if it does not exist it's probably an internal server error
  res.status(err.statusCode || 500).send(err.message);
});
```
- when it eventually gets to our middleware error handler, it should give the error object status code. and if there isnt one, that means that there was some server error and that should be 500
###### handling undefined errors
```js
app.use("/", indexRouter);
// app.use("/search", searchRouter);

// 404 handler for undefined routes
app.use((req, res, next) => {
  res.status(404).send("404: not found!");
});
```
- see this example, this will catch all other paths and return the 404 not found.
	- **MAKE SURE YOUR ROUTER IS USING ROUTER.GET AND NOT .USE OR ELSE IT WONT WORK**


##### The next function
```js
const middleware1 = (req, res, next) => {
  console.log("Middleware 1");
  next(); // Pass control to the next middleware
};

const middleware2 = (req, res, next) => {
  console.log("Middleware 2");
  res.send("Response from Middleware 2");
  // request-response cycle ends here
};

const middleware3 = (req, res, next) => {
  console.log("Middleware 3");
  res.send("Response from Middleware 3");
};

app.use(middleware1);
app.use(middleware2);
app.use(middleware3);
// will log `Middleware 1` -> `Middleware 2` and send a response with the text "Response from Middleware 2"
```
- remember that the order that they are defined matters, you register them each by invoking them and the next(); allows the next one invoked to take over
- also remember that the `res.send()` will end the req/res cycle so the third middleware will not run
###### next arguments
- `next()` no arg - simple, it will just pass on control to the next middleware
- `next(new Error)` will pass control directly to the error middleware function. skips all handlers remaning unless they are handlers for errors
- `next('route')` pass control to the next route handler with the same matchig path if present. 
	- this only works for app.METHODS or router.METHODS
	- could be the same as called next with no argument
- `next('router')` - skips all middleware fns attached to the specific router and hands control out of current router instance to the parent router (`app`) (express app is just another router under the hood)
- last two are very rare and specific use cases
- if you do not call `next()` in your router, your reqeust can hang because you're not telling express to move on to the next thing

#### Basic structure of a real world express app
```js
const express = require('express')
// ...all imports & requires here

const app = express()
const PORT = 3000

// add middlewares
app.use(helmet())
app.use(compression())
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(cors())
app.use(fileUpload())

// add router middlewares
protectedRouter.use(authMiddleware())
adminRouter.use(adminMiddleware())

// add routers
app.use('/', publicRouter)
app.use('/protected', protectedRouter)
app.use('/admin', adminRouter)

// register APIs
registerApis(publicRouter, protectedRouter, adminRouter)

// add error handlers
app.use(errorHandler404)
app.use(notifyErrorHandler)
app.use(globalErrorHandler)

app.listen(port, () => console.log(`Realworld app listening on port ${port}!`))
```
- remember that the order of the registers of middle ware and routers matters to avoid unexpected behaviors. also notice  that as such the error handlers are at the very bottom to ensure they are the last thing to run to catch all errors from previous middleware
##### .use() method
- used for registering router, middlewares, routers and error handlers. 
- can be used with or without a path as first param
- both `App` and `Router` has a .use() method
- important considertations: 
	- you can use .use() for everything but if the order of the methods is jumbled it leads to broken or unexpected behaviors
	- App is really just another Router, its a root level Router
##### what is in a router?
1. handle() function - what pro esses all the requests received by the router
2. Layer-stack - layers registerd on the router. every layer has a `path` and its own `handle` function.
	- every time use() method used on express app or router, creating a new layer in the routers stack.
###### Layers
- Layer can be one of the following: 
	- Middleware - fn with the signature `func(req, ress, next)` usually runs code, modifies the req or res and at the end, either sends the response or calles the next layer.
	- Route - also has the  `func(req, res, next)` but consists of the actual Request handlers for one or more http method types (get, put, post). it also typically hs the business logic to process the request and send response, it can also throw the error or call the next func with error as first param
	- Error handler - handles errors thrown by previous layers and has the form of `func(error, req, res, next)` as reminder, it must hav ethe four params to differentiate between error handler and middleware
	- another Router - another mini app it is both contained in a layer and has its own stack of layers. leads to nested structure of Routers that allows us to create modular mini apps created by invoking Router() on express object. 
##### Handling requests
- request is actually handled by: 
	- iterating the layer stack - loops through the layer stack and calls the handle funciton on every layer with a matching path
	- path matching - matching the path in `.use(path, handler)` with the request url. when one is not provided it will default to the root path of the Router. 
		- reminder that the path in Router extends that of the parent router, so from app (app/router/id)  inside the router would be (/id)
		- also reminder that if it defaults to root, then all requests reaching the router will all match 
	- nested layers - app / can nest to route at /admin which can then nest again at /admin/:id (relative to app root path)
	- Error handling- error handling middlware/funcs are the same stack as middlewares routers, and routes. 
		- each handle function of any layer is called by a wrapper function either a`handle_request` or `handle_error`. it also has an internal layerError variable that is initialized to null and when something is passed as obj through the next() method, its stored in that layerError variable. 
			- when the object passed in next() is errored state, Router will switch to calling <strong>handle_error</strong> instead and will only call the error handler 
##### Example Router with Middle ware and controller

```javascript
const { Router } = require("express");
const searchController = require("../controllers/searchController.js");
const carRouter = Router();

const searchValidator = (req, res, next) => {
  const value = Number(req.params.category.slice(1));
  console.log('value is', value);
  if (isNaN(value)) {
    console.log("there should be an error triggering")
    throw new Error("Invalid search parameter");
  } else {
    next();
  }
}

const searchMethodMW = (req, res, next) => {
  const { method } = req.query;

  if (!method) {
    next();
  }

  console.log("we have method content of: ", method);

  if (method === "remove") {
    // trigger search controller method for remove
  }
}

const fetchResMW = (req, res, next) => {
  searchController.getByFilters(req, res);
}

const errHandler = (err, req, res, next) => {
  console.log(err);
  res.status(404).render(
    "404", {
    err: err
  });
}

//
// ALL ABOVE ARE MIDDLEWARE FNS 
//

carRouter.get("/", (req, res) => {
  searchController.getAll(req, res, "cars");
});

// route for searching
carRouter.get(
  "/search/:category",
  searchValidator,
  searchMethodMW,
  fetchResMW,
  errHandler
);
```
- notice that this router is first defining middleware functions that it will use for a specific path '/search/:category' then notice that instead of using carRouter.use() and listing all the middle ware, I just put the middleware sequence in the .get() after the path to match. I suppose that it does not always have to be (req, res) but more so just pass through handlers. 
- also notice that error handling both renders a custom ejs page and also sets the server status code to 404 and pass the error message to the page to display. 

### Views
- in order to render dymanic html content, we use template engines to inject dynamic data to the html files we send back. 
#### Getting started
`npm install ejs`
- create subfolder in root called views
- create the skeleton express app and run `app.set`
```js
const path = require("node:path");
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "ejs");
```
##### Ejs syntax
-  `<% %>` tags allow to use javascript
- this allows us to write conditional statements, for loops, and use variables
```js
<% const animals = ["Cat", "Dog", "Lemur", "Hawk"] %>

<ul>
  <% animals.map((animal) => { %>
    <li><%= animal %>s are cute</li>
  <% }) %>
</ul>
```
- similiar to how you might use map in react to output html, you can do that with this

###### using EJS with Express
- first create an EJS template (e.g `index.ejs`)
- to display, hit it with a `res.render("viewname)`

### Deployment
what is the difference between hosting on github and a more robust hosting platform?
	- github pages is fine for hosting static web pages but will not work for dynamic nodeJS app
	- NodeJS and dynamic applications require server usage and complex server application which gh pages does not have
	- the same can be said of netlify and vercel, they do not have options for server/database operations, not good tools for the backend
	- people like AWS, Googlecloud Azure big complex cloud providers to 
		- PaaS providers (heroku, railway render, fly.io)
##### Static vs Dynamic
 - static - prewritten html css, js pages. 
 - dyanmic - templates are html might be prewritten but the actual content is not always the same for every user. for example (youtube will give content based on the users you follow, preferences)
	 - dyanmic require complex server applications
##### What is PaaS?
platform as a service - specific kind of hosting provider that handles alto fo the low-level server infrastructure that allow developers to focus on their content and not the server configuration and implementation details
	- its like a landlord who takes care of utilities, maintenance and security so we can focus on getting furniture, decorating, and living in the space. 
	- allows average everyday developers to avoid having to learn specialized server management and maintenance knowledge
- How do they work?
	- PaaS providers give you virtual 'instances' which are virtual computers that run the app. its like having your computer run the app on local host
		- having multiple instances is like having sevaral copies of your app running simultaneously which allows you to handle more traffic
		- You can support a lot of traffic with a single instance so more often than not, a single instance should be more than enough. 
			- many PaaS will give you your first instance for free
	- PaaS also give you databases, they do all the configuration and set up for you
		- some even do automatic backups for you
	- Doman names - the PaaS will give you a randomly generated domain name, and if you want to create a custom domain, you'll ned to buy one from a registrar like Porkbun or namesilo
		- you can look for new domain using domainr
		- PaaS will have documentation on how to point your new domain name with your application
	- Error handling - this is where git skills will come in handy. `git log` and `git checkout` will help to revert to different versions of the app that were working better
	- what service do I use?
		- Adaptable.io

### Forms and Data Handling
- POST vs GET - post is generally more secure becuase sensitive information is kept out of the URL which means it wont show on server logs. 
	- GET is for forms that will not modify data
- What is the PRG (Post/Redirect/Get) design pattern? this is when you generate a new or updated view wit the contorllers response and redirect the client.
##### Validation and sanitization
- what are the two steps that should be considered before going off to our server?
	- *validation* - checking for meeting required criteria (required fields, correct format)
	- *sanitization* - cleaning user input for potentiallly malicious data from being processed by removing or encoding potentially malicious characters
-  `express-validator` - the package we can use to help with sanitizing and validating
###### getting started with express-validator
`npm install express-validator`
- in your app file, `const { body, validationResult } = require("express-validator");`
- **body()** - allow you express which fields need validation, and sanitization and how t handle it (one body for each)
```js
[
  body("birthdate", "Must be a valid date.")
    .optional({ values: "falsy" })
    .isISO8601() // Enforce a YYYY-MM-DD format.
];
```
- notice that this is wrapped in an arrray. do not yet know the purpose of this. 
- also notice that you can chain selectors and can make things optional but the falsy bit means that if its not undefined or null/ false/ 0 it iwll be validated and check for the correct date format
```js
[
  body("name")
    .trim()
    .notEmpty()
    .withMessage("Name can not be empty.")
    .isAlpha()
    .withMessage("Name must only contain alphabet letters."),  
];
```
- notice here that you can a) chain multiple validators and b) have a error message for each validator that is specific to the validation field
###### escaping user input
- a form of sanitization is considering the possibility that a form that does not limit the characters you can enter would then hypothetically allow for javascript to be passed and would be run if the output does not feature a way of escaping certain characters that would in specific sequence be run as a script.; 
	- this is known as cross-site scripting (xss) attack
	- this is related to the ejs character `<%- %>` this is non escaping that will read the js as it comes, used for raw html output
		- they're used for includes in ejs templates (`<%- include('user', {user: user}); %>`)
		- because the html will  be injected in there and you cannot have the escaping apply with the html, 
	- the solution to this is to escape the output using `<%= %>` this converts html characters into strings and are harmless
 - *why is not sanitized as it comes in with the .escape() at the end of the body()?* - because its not necessary, that html is harmless in sql and viceversa, there might be contexts in which you dont want that double escaping characters which would render the supposed text all wonky
 - in web security, when we're talking about escaping, we are actually talking about encoding
 - *encoding* - involves replacing special characters with aa different representation
	 - encoding html involves using html entities
		 - character reference - a pattern of characters that represent and refer to another character (&lt;) -> (<)
		 - another example is url encoding, / usually means path seperator in url but if you mean literally / character you have to use %2F
		 - urls use % + hexadecimal number that equates to the ascii code for that character
- good sanitation should be reversible!
	- w

###### validation results
- once the validation rules are applied, you can use validation result to handle any validation errors:
```js
const controller = (req, res, next) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).render("index", {
      errors: errors.array(),
    });
  }

  // do stuff if successful
  res.redirect("/success");
};
```
- what this says is that if the array of errors is not empty then return a 400 on the response, and if the arrray is empty then redirect with the /success path
###### validation in the real world
- odin shows the validation methods inside the controllers for the app in MVC pattern. an example might look something like this: 
	- 
##### forms and express routes
- what does the `app.use(express.urlencoded({ extended: true });` do?
	- it is a middleware method that will automatically pass the http header from forms into the req.body so we can actually access the form fields.
		- express by default cannot parse the content-type http header that it comes in by default.
		- when extended is false the server wil only accept a string or an array of data, 
			- setting it to true will add some flexibilty in what it can accept
	- Content-type must match `application/x-www-form-urlencoded` because if not, server will show the data as an empty object 
### Authentication Basics\
**parking lot on authentication**
- what are the options for in the app.use(session()) object?
	- what does the secret do and what considerations do yo uneed to make when setting one?
	- how does the session.serialize user actually commit an authenticated user into the session?
	- the req.user property is added after authentication but where does that information travel in its lifespan? does it get attached to the browser in the form of a cookie? what is the difference between this and a cookie? 
	- what is the difference between req.user, local.user and connect.sid?
	- in what instances do you need to create sessions using tables in a db and what occasions do you only  need to use cookies and hashing of the password?
##### concepts in authentication
- authentication options:
	- session
	- json web tokens
	- both of these above rely on confirming who the user is to authenticate
	- Oauth and oauth protocol
		- google authentication 
		- separate components 
		- this is more about authorization
		- what does this user have authorization or access to. 
		- more complex to implement
##### packages you'll need: 
`npm install express express-session pg passport passport-local ejs`
- setting up the session and passport required modules:
```js
/////// app.js

const path = require("node:path");
const { Pool } = require("pg");
const express = require("express");
const session = require("express-session");
const passport = require("passport");
const LocalStrategy = require('passport-local').Strategy;

const pool = new Pool({
  // add your configuration
});

const app = express();
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "ejs");

app.use(session({ secret: "cats", resave: false, saveUninitialized: false }));
app.use(passport.session());
app.use(express.urlencoded({ extended: false }));

app.get("/", (req, res) => res.render("index"));

app.listen(3000, () => console.log("app listening on port 3000!"));

```
##### main components of authentication and how it works
- starts with having app use the express session object and setting up options to define session behavior
- app.use(passport.session()) to initialize the passport and session middle wares
- passport.use() to define what strategy you are going to use for authentication
- two functions (passport.serializeUser() and passport.deserializeUser()) will take the user found from searching db with your matching password and pass the id to make the cookie which is stored in the browser automatically by passport. 
	- the second one will be run when passport wants to pull from the database the user information based on a matching session from an existing cookie. the deserializer will then attach this user information to the req.user property to be used throughout different requests in this session. 
- on a log in post route, you run passport.authenticate() which automatically uses the strategy you defined to authenticate and the cookie will be generated automactially. 
- once the coookie is made, on subsequent requests, you can check for req.user and if that is present you are still logged in and can handle logic throughout your application based on this state 
##### passport
- website: http://www.passportjs.org/
- extended manual bc the main site documentation is lacking: https://github.com/jwalton/passport-api-docs
- video series YT explaining more configuration 
- What it is: a middleware that is injected into an express app that handles all the authentication logic. 
	- uses 'strategies' to authenticate
- it's really a framework where people can develop 'strategies' to authenticate that are the middleware
- On a higher level how it works is its a middleware that takes the http request object and checks what strategy you are using and then based on the strategy checks the request to determine if the user is authenticated
###### deep dive on passport and how it works
- what is happening when you import passport? 

- passing messages to redirects: express-flash, will work with passport to pass error and sucess messages to ejs. first you need to hit up the app.use(flash()) somewhere in that middle ware chain. then you hit it with that `done (null, false, {message: 'password incorrect'})` this would be placed on the authentication middleware for example when authentication function is defined and checking for invalid credentials
	- then you would follow it up in ejs with : `if(messages.error) => locals.messages.error`
	
###### http headers 

- request vs response headers - request headers are put together by the browser and are instructions to the server on what kinds of data that we the client can accept. 
	- you can have cookies and all kinds of data. you can also modify what things are in the request header
	- theresponse header includes instructions from the server to the client such as what kind of data it responded with
- cookies - both the request and response headers had cookie headers. this is because it allows memory on what the user is doing. this is needed because the http protocol is stateless meaning that it forgets what the user is doing. no way to permeate sessions. 
	- the cookies can be set by the response headers and are added to the cookies tab under application and will stay there until they expire, at which point you would need to log in again. common cookie expiration is two weeks.
cookies vs sessions, what is the difference? - cookies stored on the client browser and will attach itself the http request. Sessions are stored on the server side. on the expressjs application. 
- cookies cannot store alot of information so the session stores a bit larger data types
- benefit of session is authentication on the server side with secret key. cookies can be exposed 

##### securing passwords with bcrypt


##### getting set up with authentication
###### the core components and sequence of authentication middleware


### Prisma ORM
get started: `npm install prisma --save-dev @prisma/client`
- what is an object relational mapper?
	- it is an abstraction layer that takes out the need to write raw sequel infavor of a delcarative syntax where under the hood it will convert to raw sql and interact with your database
		- it will hook up to a postgres database and handles all the sql under the hood and generates classes that the prisma client object can interact with to query things you need. 

#####  main components of Prisma
###### prisma schema
- new way to write the schema for your database
```js
model Message {
   id        Int      @id @default(autoincrement())
   content   String   @db.VarChar(255) 
   createdAt DateTime @default(now())
   author    User     @relation(fields: [authorId], references: [id])
   authorId  Int     
}

model User {
   // user's fields
}
``` 
- notice that it has like a class 'model' which represents table
- 'id, content', etc represent the column names after is the data type and following that are attributes that you can add to those columns that define relations with other tables or other important metadata about the column created
- whenever you modify your prisma schema file you run `npx prisma generate` and it will automatically run the sql to update your tables as well as update the prisma client class so that you can use dot notation and even autocompletion with regular javascript to select tables and run queries
###### prisma client
- almost a separate library that is dynamically generated every time you run that npx prisma generate command when your prisma schema file updates. 
```js
// instantiate the client
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();

// when creating a new message
await prisma.message.create({
   data: {
      content: 'Hello, world!',
      authorId: 1
   }
})

// when fetching all messages
const messages = await prisma.message.findMany();
```
- notice here the import statement and instantiating the prisma client class
- also note the way that it inserts into the db a new row and you use object notation with key value pairs for entering data into the columns
###### connecting to a database with prisma
- before you can query with prisma, you have to make a special prisma schema file that contains your 'models' or the table definitions as well as point the prisma to your postgres database
### File uploading with Multer
- what is multer?
	- middleware library that uploads files to local storage
	- attached to form elements that have ecoding of mulit-form
	- defaults to a folder insdie the root directory of your project but you can also store the file contents in memory or a buffer to be uploaded to a cloud