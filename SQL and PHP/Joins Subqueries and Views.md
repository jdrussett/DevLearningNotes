# Joins Subqueries and Views

## Joins

---

`JOIN`: a relational operation, used with `SELECT` command, that causes two or more tables with a common domain (such as primary key-foreign key relationships) to be combined into a single table/view

- Several types of joins:
  - `NATURAL JOIN`: common columns are joined based on equality, common columns appear only once; "de-normalizes database" and will show all matching information for chosen tables
    - Example:

          SELECT column_name [or *]
          FROM table1_name 
          NATURAL JOIN table2_name;

  - `INNER JOIN`: common columns are joined based on equality, common columns appear redundantly in results
    - Have to use `ON` command with column joining
    - Using the word `INNER` is optional; SQL interprets inner joins as the default
    - Commonly use the trick of renaming tables using aliases (mentioned in section 2, Data Manipulation) to shorten queries
    - `JOIN` involves multiple tables in `FROM` clause
    - `ON` clause performs equality check for common columns of two tables
    - Matches primary keys & foreign keys, only returns rows from each table that have matching rows in the other table
    - Example:

          SELECT column_name(s) 
          FROM table1_name [table1_alias]
          INNER JOIN table2_name [table2_alias] 
          ON table1_alias.column_name = table2_alias.column_name;

  - `EQUI JOIN`: same as an inner join except joins are made using an equality operator
    - There actually is no `EQUI JOIN` command in SQL; just formatted using equality operator
    - Example:

          SELECT column_name(s)
          FROM table1_name [ table1_alias], table2_name [table2_alias]
          WHERE table1_alias.column_name = table2_alias.column_name;

  - `OUTER JOIN`: rows that do not have matching values in common columns are included in the result table (non-matching rows have null values)
    - `LEFT OUTER JOIN`: causes data from table referenced by `FROM` operator to appear even if there is no corresponding data from table referenced by `JOIN` operator
    - `RIGHT OUTER JOIN`: causes data from table referenced by `JOIN` operator to appear even if there is no corresponding data from table referenced by `FROM` operator
    - Example:

          SELECT column_name [or *]
          FROM table1_name [table1_alias] 
          [LEFT or RIGHT] OUTER JOIN table2_name [table2_alias]
          ON table1_alias.column_name = table2_alias.column_name;

    - From above, left joins would display all data, matched or not, from table 1; right joins would display all data, matched or not, from table 2
  - `SELF JOIN`: same table is used on both sides of join, differentiated using aliases
    - In all other joins, using aliases is optional; but for self joins it is mandatory
    - Need to select at least some fields from table with each alias
    - Example:

          SELECT alias1.column1, alias1.column2, [...], alias2.column1, alias2.column2, [...]
          FROM table_name alias1
          JOIN table_name alias2
          ON alias1.column_name = alias2.column_name; 

- More than two tables can be joined at a time
  - Have to join tables "in order based on how linkages would occur"; i.e. tables with similar columns
- When joining tables using typical `ON` command, it doesn't matter which table comes first/second in the equality statement
- A helpful process for multiple joins is to look at the ERD and see how the tables are linked with foreign key/primary key pairs, and this will show you how to join the tables
  - Example:

          SELECT alias1.column_name, [...], alias2.column_name, [...]
          FROM table1_name alias1
          JOIN table2_name alias2
            ON alias1.column_name = alias2.column_name
          JOIN table3_name alias3
            ON alias2.column_name = alias3.column_name
          JOIN table4_name alias4
            ON alias3.column_name = alias4.column_name
          [WHERE conditional_expression];

## Subqueries

---

**Subquery**: placing an inner query (like a `SELECT` statement) inside an outer query

- **Non-correlated query**: inner query processed before outer query; could be run on its own
- **Correlated query**: inner query uses data accessed by outer query
- Example *(general)*:

          SELECT column_name(s) [or *]
          FROM table_name
          WHERE column_name IN (SELECT DISTINCT column_name FROM table_name);

  - Query inside parentheses is the inner query, query pertaining to the original select statement is the outer query
- Options for inner query placement:
  - In a condition of the `WHERE` clause of the outer query
  - As a "table" of the `FROM` clause
  - Within the `HAVING` clause
- Non-correlated subqueries:
  - Do not depend on data from the outer query
  - Execute once for entire outer query
  - Process completely before outer query
  - Example:

          SELECT column_name
          FROM table1_name
          WHERE column_name IN (SELECT DISTINCT column_name FROM table2_name);

- Correlated subqueries:
  - Make use of data from outer query
  - Execute once for each row of data captured by outer query
  - Can use `EXISTS` operator, which returns `TRUE` if the subquery results in a non-empty set, otherwise returns a `FALSE`
  - Example:

          SELECT DISTINCT column1_name
          FROM table1_name table1_alias
          WHERE EXISTS (
            SELECT column2_name
            FROM table2_name table2_alias
            WHERE table1_alias.column2_name = table2_alias.column2_name
            AND column3_name = 'value'
          );

> - **Note**: using a subquery allows you to use aggregate functions in the outer query's `WHERE` clause; subquery can be an aggregate function with an alias name & can be used in outer query; subquery can form derived table used in `FROM` clause of outer query

- Sometimes (usually) a subquery/join can accomplish the same thing in SQL
  - Join example (specified):

          SELECT name, street, city, state, zipcode
          FROM customer c
          JOIN orders o ON c.customer_id = o.customer_id
          WHERE order_id = 8;

  - Subquery example (specified):

          SELECT name, street, city, state, zipcode
          FROM customer
          WHERE customer_id IN (
            SELECT customer_id
            FROM orders
            WHERE order_id = 8
          );

## Views

---

**View**: virtual or materialized table based on a select statement of other tables/views that provides controlled access to tables

- Example:

          CREATE [OR REPLACE] VIEW view_name AS SELECT_statement;

- **Dynamic view**:
  - A "virtual table" created dynamically upon request by a user
  - No data is actually stored; instead data from base table is made available to user (base table is the table containing the row data accessed by the view)
  - Based on SQL select statement on base tables or other views
- **Materialized view**:
  - Copy or replication of data
  - Data is actually stored
  - Must be refreshed periodically to match corresponding base table(s)
