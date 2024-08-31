great interactive course for the different keywords: https://www.sqlteaching.com/#!and
great interactive course for advanced sql topics such as mathematical functions: https://www.sqlcourse.com/advanced-course/mathematical-functions/
#### getting started with sql
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
		 - this will give you the number of distinct titles from the table shows. you can chain commands. distinct meaning that if you get repeating of the title you're selecting, it will ignore the repeats
	- the idea is that you're specifiying what data you want to see by chaining these commands in ways that will net what you want. 
- more commands include: 
	- WHERE - filter out data can meet conditionals
	- LIKE - accepts similarities:
```sql
SELECT name FROM world
  WHERE name LIKE '%land'
```
``
	- ORDER BY - sorting 
			- `SELECT language, COUNT(*) FROM favorites GROUP BY language ORDER BY COUNT(*) ASC;`
				- with order by , you can have multiple ordering criteria that will be looked at if the first criteria results in two of the same kind. for example:
					- `SELECT title FROM shows WHERE rating > 2 ORDER BY rating DESC, title ASC;` also theres `DESC`
						- what this will do is if you have two titles with the same rating, it will look at instead the title column to order them. 
		 
	- LIMIT - limit # of items displayed if you dont need to see it all
	- GROUP BY - organize the information by number of instances of repeating items
		- `SELECT language, COUNT(*) FROM favorites GROUP BY language;`
			  - what this does is selects two seperate columns and displays the total count of instances of each language
	- 
##### getting overview of the database
- you can see how the db is organized with the `.schema` command and even do `.schema tablename` for a specific table
##### Creating a table
```sql

CREATE TABLE todo_list (id INTEGER PRIMARY KEY, item TEXT, minutes INTEGER);
```
##### Inserting rows into a table
```sql

INSERT INTO store VALUES (0, "Kyosho inferno", 400);
```



inserting rows into SQL `INSERT INTO favorites (language, problem) VALUES('SQL', 'Fiftyville')` 
	- where favorites is the table name, and language, problem are separate columns and VALUES are comma separated inserted per the order columns were listed prior
	- inserting dynamically with variables: have to use strings (but not formated strings)
#####deleting data from Sql
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
##### how to add a column: 
```sql
ALTER TABLE table_name ADD COLUMN column_name column_type;
``` 
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
- *The difference between IN and =* 
	- IN is used when you have multiple results whereas = is for when you know that there will be only one result. for example if you're querying all the shows steve carrel is in, you can use = for the person_id = because there will be only one person id for the actor steve carrell
	- you can also use the IN keyword for searching for more than one row to pull data from for example when looking for data for both bradley cooper and jennifer lawrence
##### Testing .sql files with sqlite3
- you need to pipe the contents of the .sql file into the sqlite. so you can run `cat filename.sql | sqlite3 movies.db`
- alternatively, you can also run: `cat filename.sql | sqlite3 movies.db > output.txt` 
	- this will output the results in a text file so that you can see how many lines your query takes up

##### Joining a Query from two different tables
- you need the keyword JOIN (though you can achieve similar effect without join keyword)
- what does JOIN do and how do you use it?
	- allows you to create a temporary table that merges at a specific point and displays all the information. 
	- joins at the point where they are the same like show id and show_id
- ex: `SELECT title, rating FROM movies JOIN ratings ON movies.id = ratings.movie_id WHERE year = '2010' ORDER BY rating DESC, title ASC;`
	- after select you still will enumerate the columns you want from BOTH tables you're joining or however many tables you're joining. then you'll do the `JOIN othertablename ON firsttable.primaryKey = secondtable.foreignKey` 
		- the = is what the query will look for to join the tables 
		- then after the join statement you could add the filters and ordering, grouping commands you need.
###### different kinds of JOIN
- `INNER JOIN`: produces only tyhe set of records that match in both or all tables 
	- aka `JOIN` if you do just join its the same as inner join
- `FULL OUTER JOIN`: produces the set of all records in both or all tables with matching records where available. if no match, it'll show null
- `LEFT OUTER JOIN`: produces all records from the first table with matching records where available from the second table  and if no match, null
- `CROSS JOIN`: joins everything to everything and is not recommended for large tables
- visual on these : https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/
- more detailed info: https://www.w3schools.com/sql/sql_join.asp

###### using the AS keyword
used to give an alias to a column in order to add specificity to results from a query: 
`SELECT MAX(users.age) AS highest_age FROM users` this will return a column called highest_age with the maximum age on it. 
###### using the AND keyword
	- the and can be used to search for criteria that are both present in order to return that data example: 
```sql
SELECT title FROM movies
   ...> JOIN stars s1 ON movies.id = s1.movie_id
   ...> JOIN people p1 ON s1.person_id = p1.id
   ...> JOIN stars s2 ON movies.id = s2.movie_id
   ...> JOIN people p2 ON s2.person_id = p2.id
   ...> WHERE p1.name = 'Bradley Cooper' AND p2.name = 'Jennifer Lawrence';
```
	- here the goal is to get results back for titles that have both actors and as such need to have a table for stars and people for each of the actors due to the where statement applying to only one person. Limitation of the sql engine makes it that you have to make an instance of those tables for each person.


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

What are decoarated functions?
	- it is when you have a function that you want to adjust its functionality but you dont want to change the original source code. used in the context of web development for requiring a login  to access a specific route. involves something called wraps. need to know more on this. 

What do the autoincrement fields do in Sqlite tables?
	- the autoincrement field will create a separate table that will track the row ids for rows as they are added and deleted to make sure that there will always be a unique row id for each of the elements. 

What does the UNIQUE keyword do?
	- when making a table, giving something the UNIQUE keyword will ensure that the elements in that column will not have a repeating number or similar characteristic. if it does, sqlite will throw an error see app.py in finance folder in cs50 for context
Indexing unique vs non unique:
		- Unique:
		- Non-Unique: this allows a column to have rows that have the same index value for more rapid queries. it will however take longer to insert and update. 
```sql
CREATE INDEX index_name ON table_name(column_name);
```

Adding quantities in columns and grouping them by names
```sql
SELECT symbol, SUM(quantity) FROM purchases WHERE user_id IN (SELECT id FROM users WHERE username = 'charlesvill') GROUP BY symbol;
```

What does the HAVING clause do?
- used in the context of SELECT where will specify a condition to group by for example: 
```sql
SELECT
	column_1, 
        column_2,
	aggregate_function (column_3)
FROM
	table
GROUP BY
	column_1,
        column_2
HAVING
	search_condition;
```
- difference between `WHERE` and `HAVING`:
	- where is not able to be used when using an aggregate such as `COUNT, SUM, MAX`
```SQL
  SELECT users.id, users.name, COUNT(posts.id) AS posts_written
  FROM users
  JOIN posts ON users.id = posts.user_id
  GROUP BY users.id
  HAVING posts_written >= 10;
```
- notice that the having is at the end


### Installing PostgreSql
Once its installed on the computer, run this command to start the server
`sudo systemctl start postgresql.service && systemctl status postgresql.service`
- in order to connect it to our express application we have to set up a role / user that postgresql authenticates to be able to interact with the service. 
- you can set up a role with the same name as your linux
	- you can use `whoami` to see what the name of the linux computer is
- `sudo -i -u postgres createuser --interactive`
	- setting up user this way as a superuser helps you leverage "peer authentication" making using local database very easy
		- dont know why