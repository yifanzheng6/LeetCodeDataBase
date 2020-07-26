# 175. Combine Two Tables

## Question

Table: Person

| Column Name | Type    |
|-------------|---------|
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |

PersonId is the primary key column for this table.
Table: Address

| Column Name | Type    |
|-------------|---------|
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |

AddressId is the primary key column for this table.
 

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:

FirstName, LastName, City, State

## Solution
Easy, left join

```mysql
SELECT FirstName, LastName, City, State
FROM Person
LEFT JOIN Address
on Person.PersonId = Address.PersonId
```

# 183. Customers Who Never Order

## Question

Suppose that a website contains two tables, the Customers table and the Orders table. Write a SQL query to find all customers who never order anything.

Table: Customers.

| Id | Name  |
|----|-------|
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |

Table: Orders.

| Id | CustomerId |
|----|------------|
| 1  | 3          |
| 2  | 1          |

Using the above tables as example, return the following:

| Customers |
|-----------|
| Henry     |
| Max       |

## Solution

When filter null, use IS NULL, instead of = NULL

 ```mysql
SELECT c.Name AS Customers
FROM Customers AS c
LEFT JOIN Orders AS o
ON o.CustomerId = c.Id
WHERE CustomerId IS NULL
  ```
