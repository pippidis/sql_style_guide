# Johannes' SQL style guide

This is my personal guidelines to how i prefer SQLs to be formatted. The main goal of the style guide is to facilitate readable and maintainable code over strict code rules. None of the rules should be taken as axiomatic.

The overarching rule that should aways be worked towards is: **Readability counts**

Secondary: **It should be easy to maintain**



## Indentation and whitespaces

One of the stongest tools when formatting SQL is the use of whitespaces. And it is verry easy to make it go wrong. Generally, less is more in this regard, and overuse often makes it impossible to maintain.

### Avoid unessesary indents

Indentation is practical when writing styling your code, but if the start of the indentation is outside the screen, it does not matter. Therefor, use indents where it gives better readability, not anywhere else. 

Do: 

```sql
SELECT
COLLUMN_A, 
COLLUMN_B, 
COLLUMN_C
FROM SOME_TABLE
```

Not: 

```sql
SELECT
  COLLUMN_A, 
  COLLUMN_B, 
  COLLUMN_C
FROM SOME_TABLE
```

There are many style guides that encurages to have indents in situations like this. For small querries, it might work well, but if the number of columns in your select querry become large, it does not add to the readability. It just makes it more difficult to maintain. 


### Do not level

Some styling guidelines recomends to adjust the keywords so that they are right justified. This is a bad idea.

Do:

```sql
SELECT first_name AS fn
FROM staff AS s1
JOIN students AS s2 
   ON s2.mentor_id = s1.staff_num;
```

Not:

```sql
SELECT first_name AS fn
  FROM staff AS s1
  JOIN students AS s2
    ON s2.mentor_id = s1.staff_num;
```

It might be look good to make code like this when it is stable. However, if you want to update or need to change the code at a later point, it can get messy. Even if you have a automatic formatter, it will not be that pretty and does not add anything to the reading experience. That is what you have highlighing for. Furthermore, it makes it alot more hassle to copy and paste things. 

Example of bad things that can happen: 

```sql
SELECT first_name AS fn
  FROM staff AS s1
 INNER JOIN students AS s2
    ON s2.mentor_id = s1.staff_num;
```

```sql
     SELECT first_name AS fn
       FROM staff AS s1
 INNER JOIN students AS s2
         ON s2.mentor_id = s1.staff_num;
```


## Stucturing

When structuring the 

### Use vertical space


Do:

```sql
SELECT
-- Some group of collumns 
COLLUMN_A, 
COLLUMN_B, 
COLLUMN_C, 

-- Some other group of collumns
COLLUMN_X, 
COLLUMN_Y, 
COLLUMN_Z

FROM SOME_TABLE
```

Not:

```sql
SELECT
CLUMN_A, 
COLLUMN_B, 
COLLUMN_C, 
COLLUMN_X, 
COLLUMN_Y, 
COLLUMN_Z
FROM SOME_TABLE
```

There a


## Trailing commas



## One line - one thoght


## Use WHERE 1=1



## Comments


## Code examples


```sql
LEFT JOIN ( -- Number of ID Part 2 in for each ID Part 1
    SELECT CTP.ID_PART1, 
    COUNT(CASE WHEN ORIGINAL_TRANSACTION_INDICATOR = 'O' THEN 1 ELSE NULL END ) AS NUM_TRXN, 
    COUNT(*) AS NUM_RECORDS, 
    SUM(CTP.AMOUNT_IN_NOK) AS SUM_AMOUNT, 
    SUM(ABS(CTP.AMOUNT_IN_NOK)) AS ABS_SUM_AMOUNT,
    COUNT(CASE WHEN AMOUNT_IN_NOK < 0  AND ORIGINAL_TRANSACTION_INDICATOR = 'O' THEN 1 ELSE NULL END) AS NUM_OUTGOING,
    COUNT(CASE WHEN ORIGINAL_TRANSACTION_INDICATOR <> 'O' THEN 1 ELSE NULL END) AS NUM_NOT_ORIGINAL, 
    MAX(CASE WHEN TEXT_LINE1 LIKE 'Sumpost%' THEN TRUE ELSE FALSE END) AS IS_MARKED_AS_SUMPOST,
    MAX(CAST(ID_PART2 AS INT)) AS MAX_ID_PART2, 
    MAX(CASE WHEN CAST(COUNTERPART_ACCOUNT_NUM AS INT) < 100000 THEN TRUE ELSE FALSE END) AS HAS_A_TECHNICAL_COUNTERPART,
    MAX(CASE WHEN OP = 'U' THEN TRUE ELSE FALSE END) AS HAS_OP_U,
    MAX(CASE WHEN OP = 'I' THEN TRUE ELSE FALSE END) AS HAS_OP_I
  
    FROM CTD_PROD.SHARED.DP_CTD_RAW_TRANSACTIONS_CACHE AS CTP
    WHERE 1=1
    AND CTP.TRANSACTION_DATE = DATE '2023-06-14'
    GROUP BY CTP.ID_PART1
) AS PART2_IN_ID_PART1 ON PART2_IN_ID_PART1.ID_PART1 = CTP.ID_PART1

```
