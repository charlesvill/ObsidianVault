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
##### useful dictionaries methods: 
- `dict.keys()` when accessing members, you can generate a new list object that has the keys only 
- `dict.values()` generates object with only the values
	- if you want either of these keys or values to be a list, you need to make sure you wrap it in a `list(dict.values)` otherwise it will be treated as a dict or obj
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
- in the place of "r" it has been seen to use `newline=''`  as an optional argument to ensure consistent behavior of the way line ends are read across different computer platforms
more complex way to create dicts inside of dicts:
csv file: 
```csv
name,AGATC,AATG,TATC
Alice,2,8,3
Bob,4,1,5
Charlie,3,2,5
```
```python
csv_database = sys.argv[1]

database = []

with open(f"{csv_database}", "r") as csvfile:

	reader = csv.DictReader(csvfile)
	for line in reader:
		dna = { key: value for key, value in line.items() if key != 'name'}
		entry = { 'name': line['name'],
					'dna' : dna
				}
			database.append(entry)

print(database[0])
```
output: 
	`{'name': 'Alice', 'dna': {'AGATC': '2', 'AATG': '8', 'TATC': '3'}}`
	- notice each line in the csv file  i am first creating the dna which is its own dict with strand:count as k:v pairs
		- uses { key: value } telling the placement of the variables that are initialized in `for` `key, value` the comma separated is important because it denotes the actual key value distinction to the computer
		- uses line.items() to search through the items and if the key variable is not 'name' its added as a new key in the position noted on the line
	- also notice the entry object with two objects : name & its value , dna & the dict we created right before. 
	- what is the pu4rpose of the with keyword here?
		- this will implicate that we want the file to close automatically once we are done with it
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


#### SQL notes with file reading CSV
```python
import csv with open("favites.csv", "r") as file:
	reader = csv.reader(file)
	next(reader)
	for row in reader:
		favorite = row[1]
		print(favorite)
```
- the  part there next(reader) skips the first header line
	- the way around that is to use the dictionary reader where the first line, the header and figures out what the other columns are called. 
	- it will then create dicts instead of lists 
##### how we might count this
- we could be creating variables and initialize them as zero and create conditional logic that counts up each of the variables if it sees one of them. but thats a bit pedantic..
- better ways to do this: 
```python
for row in reader: 
	favorite = row["language"]
	if favorite in counts:
		counts += 1
	else:
		counts[favorite] = 1
for favorite in counts:
	print(f"{favorite}: {count}")
```
- how to sort these right hand column items?
	- `for row in sorted(counts, key=counts.get)`
- instead of checking for each items, you could also use the counter class methods
- what is a flat file database? all the data is stored as text files
- what is relatioal database? not just one sheet, but can be multiple sheets that have some relations whth one another. 
	- relational database has 4 basic functions Create, read, update, delete
- a sheet in a rdatabase is called a table: `CREATE TABLE table`
- we will be using sqlite3

##### getting started with sql
- create a sql database by running `sqlite3 favorites.db`
	- once you've already created the database you can run the same line to open your file again
	- you exit from sqlite3 by ctrl-d or ctrl-z.
- type .mode csv to put into csv mode and then importing from file into the database with `.import filename.csv filename`
- you can read items from a table with: `SELECT columns FROM table` syntax 
- some other commands used in sql to access data include: 
	- AVG
		- `SELECT `
	- COUNT
	- DISTINCT
	- LOWER
	- MAX
	- MIN
	- UPPER
 - example of accessing data from a table with column id and title: 
	 - `SELECT (COUNT(DISTINCT(title)) FROM shows;` 
		 - this will give you the number of distinct titles from the table shows. you can chain commands. 
	- the idea is that you're specifiying what data you want to see by chaining these commands in ways that will net what you want. 
- more commands include: 
	- WHERE - filter out data can meet conditionals
	- LIKE - accepts similarities
	- ORDER BY - sorting 
			- `SELECT language, COUNT(*) FROM favorites GROUP BY language ORDER BY COUNT(*) ASC;`
		 
	- LIMIT - limit # of items displayed if you dont need to see it all
	- GROUP BY - another way of organizing the information that comes back from query
		- `SELECT language, COUNT(*) FROM favorites GROUP BY language;`
			  - what this does is selects two seperate columns and displays the total count of instances of each language
	- 
	#### inserting rows into SQL `INSERT INTO favorites (language, problem) VALUES('SQL', 'Fiftyville')` ##### deleting data from Sql
		`sqlite> DELETE FROM favorites WHERE Timestamp IS NULL;`
		- NEVER DO 'sqlite> DELETE FROM favorites' 
- the above line would delete everything
##### conventions in SQL
- you use capital letters for sql commads
- use single quotes for string literals
##### updating the table
- if you need to make changes to the data because it needs to be cleaned, syntax: 
	- `UPDATE table SET column = value WHERE condition;`
data types in sql: 
blob- binary large object, some file of 0s and 1s
integer- just integers proper
numeric- dates and times, numbers but not necessarily numbers
real- decimal points in them 
text- strings

##### QUERY data from more than one table
- the relational part of the databases allows you to pull from different tables in structured ways. 
- for example if the songs table has the id for the artist and the artists table also has the artist id, you can make queries from both tables using the id. 
```sql
SELECT name FROM songs WHERE artist_id IN (
	SELECT id
	FROM artists
	WHERE name = 'Post Malone'
);
```
- the main part that connects them is the `IN` and the `(...)` 
	- what this is doing is selecting the songs where the artist id of songs will match up with the id of artists table. 
keywords: 
NOT NULL
UNIQUE
PRIMARY KEY - a numeric sequence  that identifies a specific table 
FOREIGN KEY - presence of primary keys in a different table that is not the specific table it identifies like the table that connects the show id with the actor id
- the presence of primary and foreign keys is what allows us to connect relationships between these tables. aka relational databases
JOIN - 

- what does it look like to link two databases together?
	- `FOREIGN KEY(show_id) REFERENCES shows(id)` 
		- this says that in the current table the datatype show_id is a primary key in the shows id which is a different table and it connects them
- what is a nested query?
	- with two tables like ratings and shows, if you want the show title for the specific rating query, you can nest a query to get custom results
- what does JOIN do and how do you use it?
	- allows you to create a temporary table that merges at a specific point and displays all the information. 
	- joins at the point where they are the same like show id and show_id