
## Hackerank, Higher Than 75 Marks

Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

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

## The PADS

Generate the following two result sets:

1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).

2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

```
There are a total of [occupation_count] [occupation]s.
```
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.


Note: There will be at least two entries in the table for each type of occupation.

Input Format

The OCCUPATIONS table is described as follows:

|Column|Type|
|------|----|
|Name|String|
|Occupation|String|

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

An OCCUPATIONS table that contains the following records:

|Name|Occupation|
|----|----------|
|Samantha|Doctor|
|Julia|Actor|
|Maria|Actor|
Meera|Singer|
...

Sample Output

```
Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.
```

**KEY** Don't forget ";" between two entries

```sql
SELECT CONCAT(Name, "(", SUBSTR(Occupation, 1, 1), ")")
FROM OCCUPATIONS
ORDER BY Name;

SELECT CONCAT("There are a total of ", COUNT(Occupation)," ", LOWER(Occupation), "s.") AS total
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY total
```
