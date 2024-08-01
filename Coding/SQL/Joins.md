#### INNER JOIN: Select records with matching values in both tables.

    SELECT a.column1, b.column2
    FROM table1 a
    INNER JOIN table2 b ON a.common_field = b.common_field;
#### LEFT (OUTER) JOIN: Select all records from the left table, and the matched records from the right table.

    SELECT a.column1, b.column2
    FROM table1 a
    LEFT JOIN table2 b ON a.common_field = b.common_field;
#### RIGHT (OUTER) JOIN: Select all records from the right table, and the matched records from the left table.

    SELECT a.column1, b.column2
    FROM table1 a
    RIGHT JOIN table2 b ON a.common_field = b.common_field;
#### FULL (OUTER) JOIN: Select all records when there is a match in either left or right table.

    SELECT a.column1, b.column2
    FROM table1 a
    FULL OUTER JOIN table2 b ON a.common_field = b.common_field;
