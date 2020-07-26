# 178. Rank Scores

## Question

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.

| Id | Score |
|----|-------|
| 1  | 3.50  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.85  |
| 5  | 4.00  |
| 6  | 3.65  |

For example, given the above Scores table, your query should generate the following report (order by highest score):

| Score | Rank |
|-------|------|
| 4.00  | 1    |
| 4.00  | 1    |
| 3.85  | 2    |
| 3.65  | 3    |
| 3.65  | 3    |
| 3.50  | 4    |

## Solution 1

Remember use " " for those names duplicated with functions

COUNT must follow () without space

```mysql
SELECT s.Score, COUNT(ds.Score) AS "Rank"
FROM Scores AS s, (SELECT DISTINCT Score FROM Scores) as ds
WHERE s.Score <=  ds.Score
GROUP BY s.Id
ORDER BY s.Score DESC
```

## Solution 2 (from discussion)

Almost the same with solution 1

```mysql
SELECT s.Score, (SELECT COUNT(DISTINCT Score) FROM Scores AS ds WHERE s.Score <= ds.Score) AS "Rank"
FROM Scores AS s
ORDER BY Score DESC
```

