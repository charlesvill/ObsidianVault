what is flask?
	- a framework, a 3rd party library
	- makes it easier to deploy webapplications using python
	- microframework because it solves smaller problems quickly without overwhelming you with a huge toolset
- what is in a flask app?
	- has a app.py
	- and a `templates/` folder that have the css files and js 
	- folder `static/` that have files that won't change often
	- file `requirements.txt` (sounds alot like npm)

- what is the import statements for Flask?
```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
	return "hello, world"
```

- here we are importing three important objects from flask library that are useful for web applications
- the `app = Flask(__name__)` is a variable that initializes the function Flask as a web application. 
	- and you are passing the current file name`__name__` as an argument for what is the script for this web application
```python
@app.route("/")
def index():
	name = request.args.get("name", "world")
	return render_template("index.html")
```
- what this is doing is return the execution of the render_template() fn and pass through it the name of the file you want to present and it will go look for the file. 
- the fn request.args has fn called .get() where looks for name key and if it doesnt have it, will default to "world"
- almost like the python equivalent to 
What is jinja?
	- a langauge for a framework that has conventions on these templates in python
	- `{{ % name % }}` what it looks like in the html

#### Static vs dynamic web applications
- static meaning that the html content was explicitly laid out by someone
- dynamic is when you have server requests and databases to fetch content for you and your html content is developed dynamically. 
- example of dynamic websites: 
	- google search = cats
	- `https://www.google.com/search?q=cats&sca_esv=8ab36c672be0c8ca&sxsrf=ACQVn0-`
		- search?q=cats
		- you can use flask fns to inject form data like a search bar for a server request. 
	- google themselves use a form for their  seach bar with a submit button for the form. so Idk why I like to make a fuchi face at that stuff. 
	What is one of the major benefits of having a framework?
		- jinja templating: 
			- when you want to have a root body whose contents will change, you can use template fillers with jinga to in herit from the root document and not have to write out duplicate html. 
			- like google searches, you have the page layout that will remain the same on multiple pages but 
##### multiple routes
- in order to have these multiple pages, you use different app routes. in the url it'll still look like `google.com/greet`
```python
@app.route("/greet")
def greet():
	name = request.args.get("name", "world")
	return render_template("greet.html", name=name)
```
- here we have a different route that gets triggered by either url change or logic that paths you there. 
- your route is triggered by the form action `action="/greet" method="get"`
- not here that the route method is not explicitly "get" however, its get by default, you need to change to `route("/greet", methods=["GET", "POST"]`
#### Syntax of templates
- you can reduce boilerplate code with templates and jinja syntax to inject html documents into a root one. 
- you want to create a layout.html file that will have the boilerplate code that shared amongst all pages
	- will have {% block body%}{% endblock %} where the content will get injected
- each unique page will have to have the line `{% extends "layout.html"%}` (like inheritance) to pull the layout boilerplate
	- then you will have same `{% block body %} content here {% endblock %}` with your unique page content in the middle. 
how to make a almost title for a dropdown menu: 
	- you have an option but you have it disabled and selected so that it cannot be selected: 
	- `<option disabled selected></option>`

#### Post and Get
- post methods on flask allow you to not display the server request like the GET method would
	- when you have an href link redirect like a url ie `/register` the method is GET. hence you will see alot of def functions have if POST then ... or else return the register.html page. because you get two options there, either you are only populating the page or you are actually for example submitting the form or something. 
- this is important if you're entering a password that you dont want displayed in the url like a google search would in a GET method post
- for post, you need to change the request fn from `request.args.get` to `request.form.get` to extract form values.
	



### what i need to review for sql: 
- importing sql database into python
- using sql objects in python and calling sql commands to write to the database
	- db variable
```python
from cs50 import SQL

db = SQL("sqlite:///froshims.db")

db.execute("INSERT INTO registrants (name, sport) VALUES(?, ?)", name, sport)
```
- here we have the db variable initializing the SQL object
	- and the writing to a db with the execute fn call and accepts args including variables that presumably fill in for the name and sport strings found in the sql command arg.
- Why do you need to place question marks as place holders in sql to avoid injection attacks?

##### what do cookies do in the role of security and validity in websites?
- cookies act like a stamp on a computer or device that presents that stamp through the browser everytime you go to a site.

##### Jinja shortcuts for dymanic web content
- for loops: if you pass through a list of dictionaries to your html page, you can use a jinja 'for book in books'
	- `{% for book in books %}{% endfor %}`
			- `{{book['title']}}`accessing variable content has double quotes and accessors for dicts use standard bracket notation
	- `return render_template("books.html", books=books)` <-- this what the line look like to pass through the list to jinja, and books is the variable that jinja parses
- 

Questions to ask: 
- what is hashing? in the context of password checking.