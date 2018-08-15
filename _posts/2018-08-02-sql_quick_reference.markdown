---
layout: post
title:      "SQL Quick Reference"
date:       2018-08-02 19:54:18 -0400
permalink:  sql_quick_reference
---

#### Create New Database

```
sqlite3 database_name.db
```

#### Create Table

```
sqlite> CREATE TABLE table_name (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER,
  gender CHAR,
  color TEXT,
  temperament TEXT,
  alive INTEGER
);
```

#### Add Column

```
sqlite> ALTER TABLE table_name ADD COLUMN column_name DATA_TYPE;
```

#### Remove Column

```
sqlite> ALTER TABLE table_name DROP COLUMN column_name;
```

#### Rename Column

```
sqlite> ALTER TABLE table_name RENAME COLUMN column_name TO column_name;
```

#### Delete a Table

```
sqlite> DROP TABLE table_name;
```

#### Insert Data

```
sqlite> INSERT INTO table_name (column_name, column_name, column_name) VALUES (value1, value2, value3);
```

Example:
```
sqlite> INSERT INTO cats (name, age, breed) VALUES ('Maru', 3, 'Scottish Fold');
```

#### Select Data

```
sqlite> SELECT column_name FROM table_name;
```

Example:
```
sqlite> SELECT id, name, age, breed FROM cats;
```

#### Select All Data

```
sqlite> SELECT * FROM table_name;
```

#### Select By Column Name

```
sqlite> SELECT column_name, column_name FROM table_name;
```

#### Select Unique Values

```
sqlite> SELECT DISTINCT column_name FROM table_name;
```

#### Select Based on Conditions

```
sqlite> SELECT * FROM table_name WHERE column_name = some_value;
```

Examples:
```
sqlite> SELECT * FROM cats WHERE name = "Maru";
```

```
sqlite> SELECT * FROM cats WHERE age < 2;
```

#### Update Data

```
sqlite> UPDATE table_name SET column_name = "new_value" WHERE column_name = "old_value";
```

Example:
```
sqlite> UPDATE cats SET name = "Hana" WHERE name = "Hannah";
```

#### Delete Data

```
sqlite> DELETE FROM table_name WHERE column_name = some_value;
```

Example:
```
sqlite> DELETE FROM cats WHERE id = 2;
```

#### Order By

Order the table rows returned by a certain SELECT statement.
```
sqlite> SELECT column_name FROM table_name ORDER BY column_name ASC|DESC;
```

Example - order the cats by age:
```
sqlite> SELECT * FROM cats ORDER BY age;
```

Example - order the cats by age in descending order:
```
sqlite> SELECT * FROM cats ORDER BY age DESC;
```

#### Order By with Limit

Selects extremes from a database table. Determines the number of records you want to return from a dataset.

Example - returns all of the cats in order from oldest to youngest, and returns the two oldest cats:
```
sqlite> SELECT * FROM cats ORDER BY age DESC LIMIT 2;
```

#### Between

```
sqlite> SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;
```

Example:
```
sqlite> SELECT name FROM cats WHERE age BETWEEN 1 AND 3;
```

#### Insert NULL

We can add data with missing values using the NULL keyword.

Example - a cat without a name or age:
```
sqlite> INSERT INTO cats (name, age, breed) VALUES (NULL, NULL, "Tabby");
```

#### Select NULL

Example - a cat without a name:
```
sqlite> SELECT * FROM cats WHERE name IS NULL;
```


#### Count

Count the number of records that meet a certain condition.

```
sqlite> SELECT COUNT(column_name) FROM table_name WHERE column_name = value;
```

Example - count the number of cats who have an ownder_id of 1:
```
sqlite> SELECT COUNT(owner_id) FROM cats WHERE owner_id = 1;
```

#### Group By

Groups your results by a given column.

Examples - aggregate results into different segments:
```
sqlite> SELECT breed, COUNT(breed) FROM cats GROUP BY breed;
```

```
sqlite> SELECT breed, owner_id, COUNT(breed) FROM cats GROUP BY breed, owner_id;
```
​
#### AVG()

Returns the average value of a column.

```
sqlite> SELECT AVG(column_name) FROM table_name;
```

Example:
```
sqlite> SELECT AVG(net_worth) FROM cats;
```

#### AVG() with AS keyword

Renaming the column name's return value - "aliasing the return value":
```
sqlite> SELECT AVG(column_name) AS new_column heading_display FROM table_name;
```

Example:
```
sqlite> SELECT AVG(net_worth) AS average_net_worth FROM cats;
```

#### SUM()

Returns the sum of all of the values in a particular column.
```
sqlite> SELECT SUM(column_name) FROM table_name;
```

Example:
```
sqlite> SELECT SUM(net_worth) FROM cats;
```

#### MIN() and MAX()

Returns the minimum and maximum values from a specified column.
```
sqlite> SELECT MIN(column_name) FROM table_name;
```
```
sqlite> SELECT MAX(column_name) FROM table_name;
```

Example:
```
sqlite> SELECT MIN(net_worth) FROM cats;
```

#### COUNT()

Returns the number of rows that meet a certain condition.
```
sqlite> SELECT COUNT(column_name) FROM table_name;
```

Example - count the total number of rows in a table that are not NULL:
```
sqlite> SELECT COUNT(name) FROM cats;
```
Example - count the number of cats whose net worth is greater than one million:
```
sqlite> SELECT COUNT(*) FROM cats WHERE net_worth > 1000000;
```

#### EXAMPLES

```
def selects_all_female_bears_return_name_and_age
  "SELECT name, age FROM bears WHERE gender = 'F'"
end

def selects_all_bears_names_and_orders_in_alphabetical_order
  "SELECT name FROM bears ORDER BY name ASC"
end

def selects_all_bears_names_and_ages_that_are_alive_and_order_youngest_to_oldest
  "SELECT name, age FROM bears WHERE alive = 1 ORDER BY age ASC"
end

def selects_oldest_bear_and_returns_name_and_age
  "SELECT name, age FROM bears ORDER BY age DESC LIMIT 1"
end

def select_youngest_bear_and_returns_name_and_age
  "SELECT name, age FROM bears ORDER BY age ASC LIMIT 1"
end

def selects_most_prominent_color_and_returns_with_count
  "SELECT color, COUNT(color) FROM bears GROUP BY color ORDER BY COUNT(*) DESC LIMIT 1"
end

def counts_number_of_bears_with_goofy_temperaments
  "SELECT COUNT(temperament) FROM bears WHERE temperament = 'goofy'"
end

def selects_bear_that_killed_Tim
  "SELECT * FROM bears WHERE name IS NULL"
end
```

#### SQL JOINS


##### INNER JOIN

Returns all the rows from both tables you are querying where a certain condition is met.

```
SELECT column_name(s) 
FROM first_table 
INNER JOIN second_table
ON first_table.column_name = second_table.column_name;
```

Example - return the name and breed of the cat along with the name of that cat’s owner:

```
SELECT Cats.name, Cats.breed, Owners.name
AS "owner_name" #aliasing the name column of owners table
FROM Cats 
INNER JOIN Owners
ON Cats.owner_id = Owners.id;
```

Result - returns all of the data in the specified columns from both tables:


##### LEFT OUTER JOIN

Returns all rows from the left, or first, table, regardless of whether or not they met the JOIN condition. The query will also return the matched data from the right, or second, table.

```
SELECT column_name(s)
FROM first_table
LEFT JOIN second_table
ON first_table.column_name=second_table.column_name;
```

Example:

```
SELECT Cats.name, Cats.breed, Owners.name 
FROM Cats 
LEFT OUTER JOIN Owners 
ON Cats.owner_id = Owners.id;
```

Result - returns all of the cats with matched data regarding owner’s name for those cats that have an owner, and an empty space in the owner’s name column for the cat that doesn’t have an owner.


##### RIGHT OUTER JOIN

The reverse of the LEFT OUTER JOIN - Returns all data from the right, or second, table and the matched data from the left, or first table.

```
SELECT column_name(s)
FROM first_table
RIGHT JOIN second_table
ON first_table.column_name = second_table.column_name;
```

If we insert a new owner into Owners table:

```
INSERT INTO owners (name) VALUES ("Penny");
```

Example:

```
SELECT Cats.name, Cats.breed, Owners.name 
FROM Cats 
RIGHT OUTER JOIN Owners 
ON Cats.owner_id = Owners.id;
```

Result - selects all of the data from the second table and only the matched data from the first table (Penny is now part of all the data from the second table).


##### FULL OUTER JOIN


*a.k.a. FULL JOIN*

Combines the result of both a LEFT and RIGHT OUTER JOIN. In other words, returns all the data from both the first and second tables.

```
SELECT column_name(s)
FROM first_table
FULL OUTER JOIN second_table
ON first_table.column_name = second_table.column_name;
```

Example:

```
SELECT Cats.name, Cats.breed, Owners.name
FROM Cats
FULL OUTER JOIN Owners
ON Cats.owner_id = Owners.id;
```

Result - includes both cats without owners and owners without cats. In other words, it includes *all* of our data.




















