# Introduction to SQL

## Introduction

Structured Query Language is special-purpose: manipulating sets of data in (typically) a relational database. Generally speaking, once youve picked up SQL it's easy to pick up other query languages. The basic standards are ANSI and ISO; this lesson will use an SQL product but stik to standards.

A **database** is a container we use to store and organize data; this means we have a more efficient way to store and retrieve data. A lot of time in enterprise, data is stored in a spreadsheet. A database is like containing data from a ton of "spreadsheets".

### The Relational Model

Relational is a way to describe data and the relationships between data entites. In a relational database, we store data in a table. Each table has a name (i.e. Contacts), and each column has a name (which has restrictions). Columns can be required, or not required. When not required, the data is output `null`.

To pull data, we must query the database by asking a question, ex "What are all the contacts that I have with a last name that starts with F?" We process this query through SQL. If we have a table with an input for "email" and we want to query a user with two emails, a relational database can cause issues.

To circumvent this problem, we approach what is called **normalization**, which is a way to design databases in such a way that we can "ask better questions" to retrieve our data. If we wanted to "normalize" our email field so it could have multiple emails, we should extract this column and give it a seperate table called "email," where we can then associate primary keys with foriegn keys to allow for multiple emails.

This is where the term "relational" comes from; in this design we have a relation between the "person" table, and the "email" table. When designing a database, we want to be able to answer the questions that we ask today, but work well enough to be able to answer the questions we ask tomorrow.

## Understanding Basic SQL Syntax

Basic syntax in SQL is known as a "SQL statement" which is sent to the database and answered by the database. An example of a SQL statement is: `SELECT first_name FROM person;`. Every SQL statement must have a semicolon at the end to be valid.

* `SELECT` is a keyword, and in this case is a command. Good practice is having keywords in uppercase, and identifiers in lowercase.
* `first_name` is an identifier.
* `FROM` is a keyword.
* `person` is an identifier.

Our keywords come from the SQL syntax and our identifiers inside the database. Further breaking this down, `SELECT first_name` is known as a **select clause**. `FROM person` is known as a **from clause** which tells the database "from where" we want to pull our selection.

### Select

The select command retrives one or more rows from one or more tables. `SELECT first_name, last_name FROM contacts;` is like saying "Please give me the first_name and last_name coloumns from the contacts table." This would return something like the following.

id | first_name | last name
---|------------|----------
1|John|Smith

### Insert

Adds one or more rows into a table; insert only works against **a single** table at a time, unlike select. If we use the table from our last example as a jumping-off point, an insert statement would look something like: `INSERT INTO contacts (first_name, last_name) VALUES ('Mike','Jones');`, where `INSERT INTO` is the actual command, then we specify the table name, then the columns we want to update, then the `VALUES` clause fills those columns in order.

The `id` column is very common in database design and is known as an "auto incrementing" column.

### Update

Modifies one or more rows in a table. This looks like: `UPDATE contacts SET last_name = 'Jones' WHERE id = 1;`, where `UPDATE` is the command clause, `SET` defines the column to be changed and the new value to modify, and `WHERE` uses a column choice and value. The `WHERE` clause is a restriction on our update statement creating a conditional, if left out the entire column would change to "Jones".

### Delete

Removes one or more rows from one table, this looks like: `DELETE FROM contacts WHERE id = 2;`, where `DELETE FROM` is the full command clause, and `WHERE` is the restriction clause.

## Querying Data with the SELECT Statement

`SELECT` proposes a question to the database, these questions might be, "Who are all of my contacts?" or "Who are all of my contacts with a first name of John?", or even "How many contacts do I have?".

`SELECT 'Hello','World';` is the most basic of select statements, where we are running a **select list** through `SELECT` to select two columns, `Hello` and `World`. The select list is part of the select clause. This doesn't select data from a database at all. Running this command will return one row within the result grid.

### The Select List

* Most of the time, it contains a list of columns from a table you want to query.
* In this clause, a FROM clause is required.
* Every column of data is split with a comma, except for the last comma.

`SELECT <column_name>,<column_name> FROM <table_name>;`.

### The Wildcard

By using the asterisk `*` in your column list, this will allow you to select every column in the list. Using this method is considered **bad practice**! It's much better to be explicit in your column selection list.

### The FROM Clause

* Defines the table(s) you want to query.

It's a good idea to "qualify" every query in your select list with a table name, rather than writing `SELECT first_name, last_name FROM person;`. In this case we'd write `SELECT person.first_name, person.last_name FROM person;`. Some databases will run this query faster, but it makes the SQL statement much more clear.

These statements can be aliased to prevent having to write more code: `SELECT p.first_name, p.last_name FROM person p;`, where our alias is the final letter after our from clause. This is even more important for multi-table queries, so the variables are clear where the data is coming from.

#### Demoing FROM

Aliasing can be further put to use using the `as` statement where you can run something like `SELECT 'Hello' as FirstWord, 'World' as SecondWord;` to import under the aliased column name.

We also can select which database  we support by using the keyword `USE`; anything following the word USE will be in the context of that database.

``` sql
USE contacts;

SELECT p.person_first_name as FirstName
FROM person p;
```

## Constraining the Result Set

Constraining the result set (parsing data) can be done in one of two major ways: the `WHERE` clause, and the `DISTINCT` qualifier. Distinct and Not Distinct are two main subsections of the qualifier.

`NOT DISTINCT` would be like asking, "What are the first names of all the people I know?", e.g. `SELECT p.first_name FROM person p`, which returns all of the name (non-distinct), and may have duplicate first names. This is the default search query.

`DISTINCT` would be like asking, "What are all the **unique** first names of the people I know?", e.g. `SELECT DISTINCT p.first_name FROM person p;`, which returns all of the unique entries in this column.

When using DISTINCT on multiple idenifiers, DISTINCT will return all distinct results from both columns, not just the first one: so if we have two of the same first names but the last names are different, both of the first names would appear. If two names are exactly the same, only one would appear.

``` sql
USE contacts;

SELECT DISTINCT p.person_first_name, p.person_last_name as FirstName
FROM person p;
```
