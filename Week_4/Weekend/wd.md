# Database

1) size
2) ease of updating
3) accuracy
4) security
5) redundancy
6) importance

# Intro to Relational Database
* Front-end `displays` and `collects` info
* Back-end `stores` info
* A `relational database` is a type of database that `organizes` **data into tables**, and `link` them `based on` defined `relationships`

# Database
* `contains` one or more `tables`
* `table` is made up of `rows` and `columns`
* `rows` have the `same columns`
* each `column` `contains data`
* `Fields` should only `contain one value`
* We need to `draw meaningful links` between the `tables` in order to `retrieve data`

# Drawing Links Between Tables
  1) `Give` each `row` in a table a `unique identifier`(primary key)
  2) `Reference` the `primary key` (unqiue identifier) `in` the other `table` to which you `want to link`
* `Primary key` is a `column` that `contains` unique `data` such that **no two users have the same data**
* primary key is called `Foreign key` in the `table` you `linked` 

# DB Things
* **Removing repetitive data across columns** (`1NF` / first normal form)
* **Removing repetitive data across rows**
* **If you want to give your users the ability to change their username, its better to add a numerical auto-incrementing "id" column to users and use that as the primary key**
* Sometimes you would have to create a new primary key if no good columns are good candiates
* Normalization should output a data that is cleanly organized according to the relational model

# Structured Query Language (SQL)
``` SQL
/*
Create a database, named 'development'
*/
CREATE DATABASE development;

/*
Create a table named "users"
RDBMS require that each column in a table is given a data type
full_name and username is of data type VARCHAR
VARCHAR is a string that can vary in width
note that full_name and username here are columns
which could be used as foriegn key or primary key
*/
CREATE TABLE users (
  full_name VARCHAR(100),
  username VARCHAR(100)
);

/*
Insert a record (CREATE in CRUD)
*/
INSERT INTO users (full_name, username)
VALUES ('Boris Hadjur', '_DreamLead');

/*
Retrieve all tweets belonging to @Dreamlead (Retrieve in CRUD)
Select the columns text and created_ at 
From the table tweets
Where a row with column username has the value _Dreamlead
*/
SELECT text, created_at FROM tweets WHERE username="_Dreamlead";

/*
retrieving + sorting by a column value
*/
SELECT * FROM grocies ORDER BY aisle;

/*
Retrieving + sorting + filtering
*/
SELECT * FROM grocies WHERE aisle > 5 ORDER BY aisle;

/*
Update a user's name (the Update operation in CRUD)
Update the user table
set the full name column value to Boris H
for the row that has "_Dreamlead" as the data / value of column username
*/
UPDATE users
SET full_name="Boris H"
Where username = "_DreamLead";

/*
Delete a user (the Delete operation in CRUD)
Delete from the users tabel
where the row has a value of "_Dreamlead" as the data for the column username
*/

DELETE FROM users
WHERE username="_Dreamlead";

/*
Aggregate function
* useful for things getting max, min, sum in database
*/
SELECT SUM(qunaity) FROM groceries;

/*
GROUP BY STATEMENT 
The group by statement groups rows that have the same values into summary rows, often used with aggregate functions
*/

SELECT aisle, SUM(quantity) FROM groceries GROUP BY aisle 

```

# Advance SQL Queries
* You can use `WHERE name LIKE 'B%'` to find the countries that start with "B".

# Entity-Relationship Diagrams
* helps us better understand how tables in a RBD are connected to each other 
* shows each table as a box
* links boxes together indicating what kind of relationship they have with each other 
* separates the info you need for each table and shows how the tables link together
* allows you to see the overall design of the db
**A ERD is a graphicial representation of the data requirements for db**

# 5 Major Parts of ERD

1) Entity
   - Represents a thing you want to track in a database (etc: person, place)
   - becomes a table in the db
  * Ex: You want to track students info in your db, you make student an entity which represents all the students 
   - Each occurances is called an instance, instance represent the record / row in a table
2) Attribute
  - describes various characteristics of an eneity, represents the column of the table
  - attribute tells you more about each instance of entity
  * Ex: having an attribute First name on an entity student  tells you more about each stuent 
  * attributes may or maynot be unqiue
3) Primary Key
  - attirbute(s) that uniquely identifies an instance of the entity 
  - alternatively, you could also make primary key in a way such that no two rows will share the same attirbute value 
3b) Composite Key
  - used in situations such that 2 attribute is needed to unqiuely identifies an instance of the entity 
4) Relationship
   - describes how one or more entites interact with each other, usuaully described in verbs
   * Ex:  Student has a phone number
5) Cardinaility
   - The count of instances that are allowed or are necessary between entity relationships 
   - How many rows you need before you can link a table to another table 
   - Ex: You wouldnt need a table of phone # in your db unless you decided student will have phones. 

# Cardinality
 `One to One`
  * You have to have at least one and only one (SIN card #, used as primary key because only have one its an attribute we could use to unqiuely identify someone)
 `Many to Many`
 * You have to have at least one, but you could have more (pokemons for pokemon trainers)
 `One to One optional`
* you dont have to have one but if you do it has to be only one (wife)
 `One to Many optional`
 * you dont have to have one, but if you do, you could have as many as you want (kids)

# Bridge Table
* Bridge table is used in combining data between two tables that have the many to many relationship while keeping the entity organized and uniquely identified
* The bridge table creates a one to many relationship between the two main tables (that you are trying to link and have many to many relationship )

# Writing SQL
* By assigning someone as the primary key, you are telling the db each row must have a unqiue value for that column
* SQL works backwards
* selecting an attribute that you are not groupying by may not yield sensible results

# Aggregate Function
* useful for things getting max, min, sum in database
``` SQL
SELECT SUM(qunaity) FROM groceries;
```

# Useful SQL things
1) `concat` function, takes in multiple arguments
2) `char_length`
3) when using `> on string`, sql compares the `length of the string`
4) `replace(f, s1, s2)`, replace the occurance of s1 in string f with s2
5) SQL `LIKE` gives you `one` specific `condition`, SQL `IN` gives you `multifple condition`
6) You could apply math concepts to sql queries to make the data interesting, for example, you could track population / area, and when you query you do population / area which will give you population density 
7) You could treat sql like the if part statement of js, evaulation and after evualation if gets you back stuff that meets that criteria, similar to entering a if statement 
8) You could be createive with your math select phase, and you then use macm logic on the query phase
9) We can use mathematical and string expressions as well as field names and constants.
10) The word `IN` allows us to `check` if an `item` is `in` a `list`.
11) The `IN` operator is a `shorthand` for `multiple` `OR` conditions.

# Advance SQL queries
* using AUTOINCREMENT in your id where it is a primary key allows the database to figure out the id when you insert
* AND have more precedence than OR in evaulating expression
* Using the result of a sql `query` `inside` of a `IN` query allows your `selection` to be `up to date` with the `table` `retrieved` from the squl query inside of the IN
* = is an exact match, where as LIKE is an inexact match if you use wildcard, making LIKE more flexible
* `where` is used on `individual` `values` in the individual `rows`, `having` is applied to the `group` `values`  