
## Hackerank, Higher Than 75 Marks

Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

Input Format

The STUDENTS table is described as follows:

|Column|Type|
|------|----|
|ID|Integer|
|Name|String|
|Marks|Integer|

Sample imput

|ID|Name|Marks|
|--|----|-----|
|1|Ashley|81|
|2|Samantha|75|
|4|Julia|76|
|3|Belvet|84|

Sample Output
```
Ashley
Julia
Belvet
```
**KEY** SUBSTR(COLUMN, LENGTH(COLUMN)-M, N)
```sql
SELECT Name FROM STUDENTS 
WHERE Marks > 75
ORDER BY SUBSTR(Name, LENGTH(Name) - 2, 3), ID
```
