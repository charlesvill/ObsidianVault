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
#### Creating tables
##### creating tables with foreign keys referencing other tables
-consider this example: 
![[Pasted image 20240914163711.png]]
- notice how stars has datatypes "show_id" and "person_id" that references the primary key id in people and id in shows respectively. how does one create that structure in your tables?

- you link or refer to other databases together by adding a creating a column detailed below
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
- one thing to note is that each role must have a database of the same name

### Using PostGreSQL
**pg node documentation** : https://node-postgres.com/
- client vs pool
	- - client is an individual connection to a DB and you manuallly manage it, you open the connection, do the query and then close it. it's fine for one-off queries but can get expensive if you have alot of queries
	- a pool is a pool of clients. a pool holds onto connections, 
		- if you run another query and you ahve a connection open, it will reuse that one or programmatically open a new one if needed.
#### getting started with PostGreSQL
- run `npm install pg`
- create a db/ folder and a pool.js and queries.js file
pool.js
```js
const { Pool } = require("pg");

// All of the following properties should be read from environment variables
// We're hardcoding them here for simplicity
module.exports = new Pool({
  host: "localhost", // or wherever the db is hosted
  user: "<role_name>",
  database: "top_users",
  password: "<role_password>",
  port: 5432 // The default port
});
```
- Look into what this should look like as environment variables - it should look like this: 
```js
module.exports = new Pool({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  database: process.env.DB_NAME,
  password: process.env.DB_PASSWORD,
  port: process.env.DB_PORT
});
```

queries.js
```js
const pool = require("./pool");

async function getAllUsernames() {
  const { rows } = await pool.query("SELECT * FROM usernames");
  return rows;
}

async function insertUsername(username) {
  await pool.query("INSERT INTO usernames (username) VALUES ($1)", [username]);
}

module.exports = {
  getAllUsernames,
  insertUsername
};
```
- notice the $1, that is known as parameterization to avoid sql injection attacks like were seen in cs50 with sqlite3 ?

#### PostGreSql conventions
- Auto incrementing ids?
	- in Sqlite you used `id INTEGER AUTOINCREMENT UNIQE` 
	- but in postgre you use: `id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY` 
		- this will ensure that the id always has a unique id number that tracks the number of rows and columns ot make sure that this goal is met. 
		- it will automatically create a 
- Property types
	- `username VARCHAR (255)` : postgresql you either fixed string or variable string. varchar is a variable string that allows for a difference in length for the string. 
		 - the 255 means the maximum length it can be. if it goes larger than that, postgre will throw an error.
		- its not really true that you need to choose one or the other for string types. you can also use TEXT just like sqlite and you can store up to 1gb of information but it's more of a way to govern the input data. not really a performance difference between the two that would be significant. 
##### How to log in to your db
- in your terminal, hit `psql` to start up postgres
- `\l` to see the current dbs in your instance
- `CREATE DATABASE <dbname>` to create one if you dont have one
- `\c <dbname>` to connect to it
	- you should see `<dbname>=#` on the command prompt
##### how to dynamically create your table schema
```js
#! /usr/bin/env node

const { Client } = require("pg");

const SQL = `
CREATE TABLE IF NOT EXISTS usernames (
  id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  username VARCHAR ( 255 )
);

INSERT INTO usernames (username) 
VALUES
  ('Bryan'),
  ('Odin'),
  ('Damon');
`;

async function main() {
  console.log("seeding...");
  const client = new Client({
    connectionString: "postgresql://<role_name>:<role_password>@localhost:5432/top_users",
  });
  await client.connect();
  await client.query(SQL);
  await client.end();
  console.log("done");
}

main();
```
- the shebang at the top is some sort of operating system note to tell it how to run this program by looking for node. not sure how necessary it is if one already has node installed globally on your computer
- but noice that it sets up a client session passing through the authentication credentials, it queries the creation of the columns and inserts some items there, and then it ends the session. 
###### populating prodution dbs
- in a production environment, this script would actually only populate the db of the local db because the local db connection was hardcoded. 
- we need a way to manipulate env variables to have the production server db to run the script
- the easiest way to do it is by providing the connection information as an argument to the script. 
	- this way it can run the script for the local db as well as production db
	- you can access arguments via process.argv
```bash
# populating local db 
node db/populatedb.js <local-db-url>

# populating production db
# run it from your machine once after deployment of your app & db
node db/populatedb.js <production-db-url>
```
- this is how it would look like to get it populated on both local and the server db
- make sure the script has argv imported so you can actually pass arguments to the script via:
```js
const { argv } = require('node:process');

// print process.argv
argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
```
then run `node process-args.js one two=three four`
and this will be printed: 
```shell
0: /usr/local/bin/node
1: /Users/mjr/work/node/process-args.js
2: one
3: two=three
4: four
```
##### first DB project
- creating a mini message board that should be able to Create, Read, Update, Delete
###### what is the 'dotenv' package for?
- in order to pass the local connection and password information to the config of the db pool, you need to import the 'dotenv' npm package to be able to read environment variables
- `node install dotenv --save`
- then in your file using enviroment variables: `require('dotenv').config()`
- then create a `.env` file so you can feed the authentitcation details from the .env file
- your variable follow the pattern `DB_HOST="localhost"` with no semi colon
- then you call them with `process.env.DB_HOST`

###### wildcard selectors in postgreSql
- in the query:  "`SELECT * FROM table WHERE column LIKE $1`", `[var]`
	- $1 indicates the number of variables passed in the array, and after that, you need to pass all the variables that will go in there
- your variable with a wildcard selector needs to be formatted to include the wild card selector as a string. then pass the formatted string as the variable: 
```js
const fQuery = `%${query}%`;
```
- reminder that the wildcard before and after means that the search has the query inside of it
*dont forget that sql using single quotes for string literals like selecting a cell member. if you use double quotes, it will think you're trying to select a column of the name of the string literal you entered.*

###### conventions with querying
- remeber that to get a query, you need to deconstruct the row from the query method `const { rows } = db.query('SELECT...');`
- also remember that it will return an array. so you either run a map method or if you're expecting a single object, you 
*passing multiple values*
- if you are inserting multiple variables, you need to make to space out every variable like this: 
```js
await pool.query("INSERT INTO messages (name, content, time) VALUES ($1, $2, $3)", [message.name, message.content, message.time]);
```