## Occupations

Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

Input Format

The OCCUPATIONS table is described as follows:

|Column|Type|
|------|----|
|Name|String|
|Occupation|String|

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

Sample Input

|Name|Occupation|
|----|----------|
|Samantha|Doctor|
|Julia|Actor|
|Maria|Actor|
|Meera|Singer|
...

Sample Output

```
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria
```
Explanation

The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.

**Solution**

```sql
set @r1=0, @r2=0, @r3=0, @r4=0;
select min(Doctor), min(Professor), min(Singer), min(Actor)
from(
  select case when Occupation='Doctor' then (@r1:=@r1+1)
            when Occupation='Professor' then (@r2:=@r2+1)
            when Occupation='Singer' then (@r3:=@r3+1)
            when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber,
    case when Occupation='Doctor' then Name end as Doctor,
    case when Occupation='Professor' then Name end as Professor,
    case when Occupation='Singer' then Name end as Singer,
    case when Occupation='Actor' then Name end as Actor
  from OCCUPATIONS
  order by Name
) Temp
group by RowNumber
```

Output

```
Aamina Ashley Christeen Eve
Julia Belvet Jane Jennifer
Priya Britney Jenny Ketty
NULL Maria Kristeen Samantha
NULL Meera NULL NULL
NULL Naomi NULL NULL
NULL Priyanka NULL NULL
```

**Key Idea**

```sql
set @r1=0, @r2=0, @r3=0, @r4=0;
 select case when Occupation='Doctor' then (@r1:=@r1+1)
            when Occupation='Professor' then (@r2:=@r2+1)
            when Occupation='Singer' then (@r3:=@r3+1)
            when Occupation='Actor' then (@r4:=@r4+1) end as RowNumber,
    case when Occupation='Doctor' then Name end as Doctor,
    case when Occupation='Professor' then Name end as Professor,
    case when Occupation='Singer' then Name end as Singer,
    case when Occupation='Actor' then Name end as Actor
  from OCCUPATIONS
  order by Name
```

Output

```
1 Aamina NULL NULL NULL
1 NULL Ashley NULL NULL
2 NULL Belvet NULL NULL
3 NULL Britney NULL NULL
1 NULL NULL Christeen NULL
1 NULL NULL NULL Eve
2 NULL NULL Jane NULL
2 NULL NULL NULL Jennifer
3 NULL NULL Jenny NULL
2 Julia NULL NULL NULL
3 NULL NULL NULL Ketty
4 NULL NULL Kristeen NULL
4 NULL Maria NULL NULL
5 NULL Meera NULL NULL
6 NULL Naomi NULL NULL
3 Priya NULL NULL NULL
7 NULL Priyanka NULL NULL
4 NULL NULL NULL Samantha
```
