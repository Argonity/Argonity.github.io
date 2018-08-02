---
layout: post
title:      "SQL Quick Reference"
date:       2018-08-02 23:54:17 +0000
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




























