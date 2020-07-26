# 184. Department Highest Salary

## Question

The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.

| Id | Name  | Salary | DepartmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |

The Department table holds all departments of the company.

| Id | Name     |
|----|----------|
| 1  | IT       |
| 2  | Sales    |

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, your SQL query should return the following rows (order of rows does not matter).

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |

## Solution 1

Three layers of subquary, seems inefficient

checked other solutions in discussion didn't find a brilliant solution.

```mysql
SELECT d.Name as Department, me.Employee, me.Salary 
FROM Department as d, 
    (SELECT e.Name as Employee, e.Salary as Salary, e.DepartmentId
    FROM Employee as e,
        (SELECT MAX(e.Salary) as Salary, e.DepartmentId 
        FROM Employee as e 
        GROUP BY e.DepartmentId) as m
    WHERE m.DepartmentId = e.DepartmentId and m.Salary = e.Salary) as me
WHERE d.Id = me.DepartmentId
```

## Solution 2

Inspired by the solution of 185

```sql
SELECT d.Name as Department, e.Name as Employee, e.Salary
FROM Department as d, Employee as e
WHERE e.DepartmentId = d.Id
AND 
    (SELECT COUNT(DISTINCT Salary) 
     FROM Employee 
     WHERE DepartmentId = d.Id 
     AND Salary>e.Salary) <1
```


# 185. Department Top Three Salaries

## Question
The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id.

| Id | Name  | Salary | DepartmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |

The Department table holds all departments of the company.

| Id | Name     |
|----|----------|
| 1  | IT       |
| 2  | Sales    |

Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows (order of rows does not matter).

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Randy    | 85000  |
| IT         | Joe      | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

Explanation:

In IT department, Max earns the highest salary, both Randy and Joe earn the second highest salary, and Will earns the third highest salary. There are only two employees in the Sales department, Henry earns the highest salary while Sam earns the second highest salary.

## Solution 1 (from discussion)

So brilliant!!!!

1. An employee's salary is in top three, if only if there are less than 3 salaries which are higher.
2. Use the common department id to compare salary, instead of use group by or partition by

```mysql
SELECT d.Name as Department, e.Name as Employee, e.Salary
FROM Department as d, Employee as e
WHERE e.DepartmentId = d.Id
AND 
    (SELECT COUNT(DISTINCT Salary) 
     FROM Employee 
     WHERE DepartmentId = d.Id 
     AND Salary>e.Salary) <3
```
