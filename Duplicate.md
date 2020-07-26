# 182. Duplicate Emails

## Question

Write a SQL query to find all duplicate emails in a table named Person.

| Id | Email   |
|----|---------|
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |

For example, your query should return the following for the above table:

| Email   |
|---------|
| a@b.com |

## Solution

Easy

```mysql
SELECT Email
FROM Person
GROUP BY Email
HAVING COUNT(Id) > 1
```

# 196. Delete Duplicate Emails

## Question

Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

| Id | Email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

Id is the primary key column for this table.
For example, after running your query, the above Person table should have the following rows:

| Id | Email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |

Note:

Your output is the whole Person table after executing your sql. Use delete statement.

## Solution 1

1. Try to avoid "select and update conflict" by using a middle table with select clause
2. delete from [table] where

```mysql
DELETE FROM Person
WHERE Id NOT IN

(SELECT *
FROM 
 (SELECT min(Id) FROM Person
  GROUP BY Email) t
 )
```

## Solution 2 (from discussion)

Compare two tables, and delete one on conditon with the relationship between two tables.

```mysql
DELETE p 
FROM Person p, Person q 
WHERE p.Id>q.Id AND q.Email=p.Email 
```
