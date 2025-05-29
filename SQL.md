SELECT: Pick which columns of your table to take

FROM: Pick which table, you can do table t1 as an alias

WITH: Creates a temporary result set that can be referenced by SELECT, DELETE, etc

AS: Alias column names

GROUP BY: Used to group rows that have the same value in specific column as well as apply aggregate functions such as COUNT, SUM, AVG to each group. It literally makes a group for each row that has that condition. 

WHERE: Used to filter data before aggregated by GROUP BY or it is just returned

HAVING: Used to filter groups after data is aggregated by a GROUP BY

COUNT: Cannot be used directly in a WHERE clause, you have to group by and then HAVING
SUM:
AVG:
MAX: Finds the max value in that column

COALESCE: Returns the first non NULL value in a list. You can give it your normal values and NULL to return NULL if there is an empty list.

JOIN: By default assumes INNER JOIN.  

OUTER JOIN: Used to combine rows to two tables including rows that do not having matching values xd.

INNER JOIN: Only returns matching rows from the two tables. 

LEFT JOIN: Returns all rows from the left table and only the matching rows on the right table. 

RIGHT JOIN: Same but for the right table 

FULL JOIN:

ON: Used in a JOIN to specify which rows to connect

DELETE: Use this instead of SELECT, you cant use group by in this. You can do a SELECT subquery in it to use the normal syntax to find the stuff to delete.

NOT IN: Seems that you can make like a sub query and then check if something is not init.

ROW_NUMBER(): Creates a ordered list

DENSE_RANK(): Creates ordered list taking into account duplicates.

DISTINCT: Only returns unique values

OVER:

ORDER BY:

DESC / ASC:

LIMIT __ OFFSET __ : Used to limit the number of rows to return and how many rows to skip before starting to return rows.

Fun Facts:
- You can't use AS alias's in a ON or WHERE clause
- COUNT( * ) counts the total number of rows in the table
- 

Question:

Examples:
``` SQL
DELETE p1 FROM Person p1
JOIN Person p2 # dups 
ON p1.email = p2.email AND p1.id > p2.id;
```

```sql
DELETE FROM Person
WHERE id NOT IN (
    SELECT min_id
    FROM (
        SELECT MIN(id) AS min_id
        FROM Person
        GROUP BY email
    ) AS Temp
)
```

```sql
WITH Ranked AS (
    SELECT
    salary,
    DENSE_RANK() OVER (ORDER BY salary DESC) AS ordering
    FROM Employee
)
SELECT COALESCE(
    (SELECT DISTINCT salary
    FROM Ranked WHERE ordering = 2
    ), NULL)
AS SecondHighestSalary
```

```sql
SELECT id,
    CASE 
        WHEN p_id IS NULL THEN 'Root'
        WHEN id IN (SELECT p_id FROM Tree)THEN 'Inner'
        ELSE 'Leaf'
        END AS type
 FROM Tree
```