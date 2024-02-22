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