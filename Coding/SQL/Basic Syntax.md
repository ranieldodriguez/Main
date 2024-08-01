# Basic SQL Syntax
#### SELECT: Retrieve data from a database.

    SELECT column1, column2
    FROM table_name;
#### DISTINCT: Select unique values.

    SELECT DISTINCT column1
    FROM table_name;
#### WHERE: Filter records.

    SELECT column1, column2
    FROM table_name
    WHERE condition;
#### AND, OR, NOT: Combine multiple conditions.

    SELECT column1, column2
    FROM table_name
    WHERE condition1 AND condition2;
    
    SELECT column1, column2
    FROM table_name
    WHERE condition1 OR condition2;
    
    SELECT column1, column2
    FROM table_name
    WHERE NOT condition;
#### ORDER BY: Sort results.

    SELECT column1, column2
    FROM table_name
    ORDER BY column1 ASC|DESC;
#### LIMIT: Specify the number of records to return.

    SELECT column1, column2
    FROM table_name
    LIMIT number;
