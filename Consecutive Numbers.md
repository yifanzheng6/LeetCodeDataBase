# 180. Consecutive Numbers

## Question

Write a SQL query to find all numbers that appear at least three times consecutively.

| Id | Num |
|----|-----|
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |

For example, given the above Logs table, 1 is the only number that appears consecutively for at least three times.

| ConsecutiveNums |
|-----------------|
| 1               |

## Solution 1 (from discussion)

It is a smart idea!

Could apply operations on the numeric columns 

```mysql
SELECT DISTINCT Num AS ConsecutiveNums
FROM Logs
WHERE (Id + 1, Num) IN (select * from Logs) AND (Id + 2, Num) IN (select * from Logs)
```

## Solution 2 (from discussion)

Need to pay more attention on how defined variables work in sql

```mysql
SELECT DISTINCT num AS ConsecutiveNums FROM
(SELECT num,
	CASE 
		WHEN @record = num THEN @count:=@count+1
		WHEN @record <> @record:=num THEN @count:=1 END AS n
    FROM 
	    Logs ,(SELECT @count:=0,@record:=(SELECT num FROM Logs LIMIT 0,1)) r
) a
WHERE a.n>=3
```

