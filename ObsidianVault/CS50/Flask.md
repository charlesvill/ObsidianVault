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

What is jinja?
	- a langauge for a framework that has conventions on these templates in python
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

#### Post and Get
- post methods on flask allow you to not display the server request like the GET method would
- this is important if you're entering a password or 


#### Syntax of templates
- you can reduce boilerplate code with templates and jinja syntax to inject html documents into a root one. 

how to make a almost title for a dropdown menu: 
	- you have an option but you have it disabled and selected so that it cannot be selected: 
	- `<option disabled selected></option>`

### what i need to review for sql: 
- importing sql database into python
- using sql objects in python and calling sql commands to write to the database
	- db variable
- Why do you need to place question marks as place holders in sql to avoid injection attacks?