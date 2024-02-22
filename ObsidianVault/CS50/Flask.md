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