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

```