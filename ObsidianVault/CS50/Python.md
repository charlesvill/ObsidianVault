an interpreted language unlike C that needs to be compiled to 0s and 1s. the program python on your terminal interprets your code and figures out how to convert it to those 0s and 1s.
- Dynamic vs static - python like javascript is a dynamic typed language that means the variable type will be determined based on the contents as opposed to having to explicitly name the type like you would in C or C++.
#### strings
- formatted strings: print(f"hello, {nameVar}")
	- this will allow you to interpolate variables with printing but need to prefix the string with the 'f' that lets python know that you're trying to add the variable in there. 
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