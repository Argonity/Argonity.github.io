---
layout: post
title:      "SQL's SELECT"
date:       2018-08-15 13:38:31 +0000
permalink:  sqls_select
---


I'm going to be illustrating an example of a complex query using **SELECT** and attempt to explain what is being achieved on each line of the query. We'll create a few tables and then structure the query to retrieve data from them.

The way I like to think about queries is to imagine your boss asking you to print out on a sheet of paper, in table format, specific information from the company's database for him/her to analyze.

Your boss is also very particluar and wants the data grouped by and ordered by a certain way. After all, what good is data if not displayed in an organized and easy to follow format?


### Example #1


Using Flatiron Learn's crowdfunding example, let's create 3 tables for your boss:

```
CREATE TABLE projects (
  id INTEGER PRIMARY KEY,
  title TEXT,
  category TEXT,
  funding_goal INTEGER,
  start_date INTEGER,
  end_date INTEGER
);
```

```
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER
);
```

```
CREATE TABLE pledges (
  id INTEGER PRIMARY KEY,
  amount INTEGER,
  user_id INTEGER,
  project_id INTEGER
);
```


Now, your boss is asking you to retrieve some specific information about the company site's users, their projects, and also the pledges made to the users' individual projects.

*"I want the titles of all projects with their pledge amounts. Oh, and alphabetize the table by the name of the projects."*

So let's think about what are table of retrieved data needs to look like: 

* Column 1: Project names
* Column 2: Pledges amount
* Sort Order: Alphabetized by project name

Seems simple enough. Let's build our query with some thought process:

It's going to look something like this:

```
SELECT title, SUM(amount)
FROM projects
JOIN pledges
ON projects.id = pledges.project_id
GROUP BY projects.title
ORDER BY projects.title ASC;
```


Let's break it down.


**SELECT title, SUM(amount)**

Here we are establishing the columns we want shown on our table. We said we needed two columns: Project names (title) and Pledges amount (amount).
	
We also have a SUM function. Well, don't we want to show the total amount for each project rather than showing its individual pledge amounts?
	 
	 For example, instead of this:
	 
	 Project Learn ..... $50
	 Project Learn ..... $75
	 Project Learn ..... $20
	 etc.
	 
	 We want the SUM of all the amounts for that individual project:
	 
	 Project Learn ..... $145

**FROM projects**

Here we are pointing to the table from which we want to obtain our columns. Remember, we need two columns: title and amount. "Title" will come from our projects table and "Amount" will come from our pledges table. But here we list our *first* table we want information from. This will give us our title column. Now we need our amount column from our pledges table...

**JOIN pledges**

Here we are telling our query to access or join-in the pledges table since we need our amount column from it. If we don't join-in this table, how will our query know from where to get the amount column? 

Now, given these are two separate tables in our database, how will they "talk" to each other? In other words, what data point will connect the two tables? Because I need to access two tables, *projects* for title, and *pledges* for amount, there needs to be a way they can access each other's data...

**ON projects.id = pledges.project_id**

Here we are connecting our two tables together so they can access each other's data. Our projects table has an `id` column and our pledges table references those individual projects from the projects table with its `project_id` column (foreign key). Now they understand *how* to join themselves.

So at this point in the query we have our two columns: Title and Amount. In the first column we  list each project title and in the second column we list the sum of its pledge amount. All that's left is to organize the data alphabetically.

**GROUP BY projects.title**

Because we used an aggregate function like `SUM`, we need to use `GROUP BY` as it sorts the result sets of our aggregate function. Just think that when you use an aggregate function, you'll need a `GROUP BY` line.


**ORDER BY projects.title ASC;**

Here we sort our table alphabetically by project title. The `ORDER BY` function defaults to ascending, so we don't really need to include `ASC` at the end of the query.

That's it! 


