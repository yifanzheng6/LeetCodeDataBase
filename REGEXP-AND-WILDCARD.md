# Hackerrank Weather Observation Station 6, 7, 8, 9, 10, 11, 12
Input Format

The STATION table is described as follows:

|Field|Type|
|-----|----|
|ID   |NUMBER|
|CITY | VARCHAR2(21)|
|STATE|VARCHAR2(2)|
|LAT_N|NUMBER|
|LONG_W|NUMBER|

## Question 6

Query the list of CITY names **starting with** vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

## Solution

```sql
SELECT DISTINCT CITY FROM STATION
WHERE city REGEXP "^[aeiou]"
```

## Question 7

Query the list of CITY names **ending with** vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

## Solution

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "[aeiou]$"
```

## Question 8

Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their **first** and **last** characters. Your result cannot contain duplicates.

## Solution

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^[aeiou].*[aeiou]$"
```

## Question 9

Query the list of CITY names from STATION that **do not start with** vowels. Your result cannot contain duplicates.

## Solution

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^[^aeiou]"
```

## Question 10

Query the list of CITY names from STATION that **do not end with** vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "[^aeiou]$"
```
## Question 11

Query the list of CITY names from STATION that **either do not start with vowels or do not end with vowels**. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^[^aeiou]" OR CITY REGEXP "[^aeiou]$"
```

## Question 12

Query the list of CITY names from STATION that **do not start with vowels and do not end with vowels**. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^[^aeiou].*[^aeiou]$"
```
