an interpreted language unlike C that needs to be compiled to 0s and 1s. the program python on your terminal interprets your code and figures out how to convert it to those 0s and 1s.
- Dynamic vs static - python like javascript is a dynamic typed language that means the variable type will be determined based on the contents as opposed to having to explicitly name the type like you would in C or C++.
#### strings
- formatted strings: print(f"hello, {nameVar}")
	- this will allow you to interpolate variables with printing but need to prefix the string with the 'f' that lets python know that you're trying to add the variable in there. 
- Common string methods: 
	- `str.split(',')` will split up the string into an array at the specific point
	- `str.strip("!.?")` will return a string with what you put into the arguments removed. 
		- if the argument is omitted, it will remove white spaces
	- for either of those two, if you put something in the arguements thats not in there, it wont throw an error it will just return the string without any changes. 
#### datatypes
- int
- float
- bool
- str
other different ones: 
- range
- list
- tuple
- dict
- set
- **You can use the type() method to see what data type something is**

#### variables
- do not use the unary incrementor variable++
- declaring conditionals and variables 
```python
varName = 0; 

if varName == 2:
	print("hi")
elif varName == 3:
	print("lol")
else: print("lmao")
```
- python does not have arrays, it only has lists
- range is used to count up list style (`ie. range(3) == 0 1 2`) 
	- range arguments: range(start, # of times, step) by step meaning if you put 2, skip count 2
- python still faces the same problem of float imprecision 
- python however does not face integer overflow if the number is too long it will just allocate more bytes of memory to make up to make the entire number 
##### taking in input in python
- 
##### evaluating expressions
to compare many things you no longer need || for the or: 
```python 

if s == "Y" or s == "y":
	print("agreed.")
elif s == "N" or s == "n":
	print("Not agreed.")
```
- you can also use `and` instead of having to use &&
- single and double quotes are virtually the same in python, no difference unlike C or C++

#### loops in python
```python
for i in range(7):
	print(meow)
```
- range prints out one at a time not all at once like C where you have to malloc the size at initialization
- there are no do while loops so you have to do while loops that intentionally induce infitite loop and have a break statement when you're sure that you have what you wanted. 
#### OOP in python
- you can access the mehtods for strings using dot notation like: `s.lower()` this would access the class of str and pull the method lower() to bring to lowercase 
- strings in python are immutable when you manipulate the string in python you really are getting a copy of the original and python will forget about the original and since you dont have to handle memory then you just forget about it too. 

#### declaring funcitons
- need to start with `def`
```python
def meow():
	something cool
```

- functions need to be defined before you try to invoke them. it's convention to make a main function and all your functions below that and then call main at the very bottom of your code
- variables declared inside of a loop in the context of a function can be used out side of the loop or conditionals so they are not bound by the same scope issues that bounds C or javascript. 
- the print function allows you to print out something multiple number of times `print("?" * 4)` 
##### try and except
you can use try to test possibly breakable things such as accepting input for a int and the user inputs a string
``` python
def get_height():
	while True:
		try:
			n = int(input("Height: "))
			if n > 0: 
				return n
		except ValueError:
			print("not an integer")
```
##### useful functions
- strings: 
	- formatted strings: 
		- interpolation: `print(f"Average: {average}")` similar to js
- for lists: 
	- length len()
	- sum sum()
		- passthrough the list name in the parentheses
	- add to list: list.append(listToAppend)
	- slicing: `argv[1:]` `argv[0:2]` the colon denotes the boundary between where to start and what value to end. if the value to the right is omitted, it will include the rest of them. I wonder if this is like the spread operator in js [[Intermediate Javascript#Parking lot for review in foundational JS]]
- for command line arguments: 
	- you need to import `sys` to get argv to get the # of arguments for the program
		- you can also get the exit code with sys.exit(1) or sys.exit(0)
#### Dictionaries
- dict objects are the same thing as objects in js
- `people = {}`

```python
	"carter": "+1-909-495-1000",
	"David": "+1-099-9349",
```
- *very similar to the use of objects in js* [[Intermediate Javascript#objects as a design pattern]]
#### File management
- first need to import `import csv`
- if youre expectig file to imported using cli, you also need `import sys`
```python
import csv
import sys

if len(sys.argv) != 2:
	sys.exit("needs two cli arguments FILENAME")
csv_file = sys.argv[1]
```
- *note* : just like in C, you can use argv to access arguments passed through terminal *reminder* : argv[0] is the name of the program so the next ones are the arguments   
- to open and load the file into memory: 
```python
	with open(f"{csv_file}", "r") as file: 
		reader = csv.DictReader(file)
		for line in reader: 
			line["rating"] = int(line["rating"]) # here dictreader creates objects using headers
			teams.append(line)
```
- note here the `with` `open` `as` and `file:` 
- it reads line by line of the csv file and creates dictionaries using the first row as the fieldnames for the objects
- optionally, if you wanted to place it into say a list, you could append each line (or now dict) into your list
##### super cool libraries to try out from python
- import pyttsx3 
```python
import pyttsx3

engine = pyttsx3.init()
name = input("Name: ")
engine.say(f"hello, {name})
engine.runAndWait()
```
- import os && qrcode
```python
import os
import qrcode

img = qrcode.make("https://youtu.be/ksldkfsj")

img.save("qr.png", "PNG")

os.system("open qr.png")
```