# Data Manipulation

**Data Manipulation Language**: commands that maintain & query a database; interact with information contained within database

- `DESCRIBE` or `EXPLAIN` will provide information about structure of chosen/designated  table, not the values/rows in that table
- `INSERT INTO` allows you to enter in new rows/records to existing tables; you can insert values into the entire table (i.e. a value for every column to contribute to the new record) or you can specify exactly which columns to add values for
  - Example: - *every column*

          INSERT INTO customer
          VALUES (1, 'John', 'Smith', '111-111-1111', 'john@smith.com');

    - Each one of the above objects enters a value for a unique column in the table
  - Example: - *subset of columns*

          INSERT INTO customer (name, email, age) 
          VALUES
            ('Robert', 'rok197@hotmail.com', 39),
            ('Leah', 'Leeyuhlater@gmail.com', 22);

    - If column is `NOT NULL`, must provide a value for that column on every record
  - Can enter in more than one record at a time into tables, separating records with commas
  - Example:

          INSERT INTO item 
          VALUES 
            (3, 'Purse', 'Leather', '$35'), 
            (4, 'Socks', 'Cotton', '$10'), 
            (5, 'Shirt', 'Polyester', '$40');

  > - Note on SQL syntax: strings of text need to be enclosed by single quotes, otherwise you will get an error
  >   - Numbers separated by things that could be determined as mathematical operations must also be enclosed by single quotes, or else SQL will interpret this as an operation (such as subtracting numbers in a phone number)

  - If you enter in values with an auto-incrementing column, neglect that column for insert statements; it will be entered automatically
- `UPDATE` allows you to change values in a column of a table; using `SET` command to identify which column, and `= value` to indicate what to change the value to
  - Use the `WHERE` conditional operator to specify exactly which, if not all, records to update for that column
  - Example:

          UPDATE table_name
          SET column_name = new_value
          [WHERE conditional_statement];

    - `conditional_statement` tells SQL which records to update the column for; i.e. `WHERE product_id = 7`, or `WHERE last_name NOT IN ('Miller', 'Peterson', 'Rose')`
- `DELETE` allows you to delete values from a table; this does not function according to column, but will delete from all columns the data for the records specified
  - Again, can use `WHERE` conditional operator to specify for which records to delete all data
  - Example:

          DELETE FROM table_name;

    - Will delete all records/data from specified table
  - Example:

          DELETE FROM table_name
          WHERE conditional_statement;

    - Will delete records from table only for which the conditional statement holds true
- `TRUNCATE` is similar to `DELETE` but will maintain table structure, remove all data & reset auto-increment counter; cannot be narrowed by conditional statements

> - Difference in syntax:
>   - `DELETE FROM table_name [WHERE conditional_statement];`
>   - `TRUNCATE TABLE table_name;`

## Query records using the following commands

---

- `SELECT` - returns all, or specified number of, columns and their values
  - Can use `SELECT *` to return all columns or `SELECT column_name, column_name, ...` to return specific columns
  - Can restrict results to rows that don't repeat according to specific column(s) using `DISTINCT`

          SELECT DISTINCT column_name

- `FROM` - identifies tables from which data will be obtained
  - Indicates which table to return values from

          SELECT column_name, ... [or *]
          FROM table_name;

- `WHERE` - specifies conditions under which row/data point will be included in the result of the query
  - Uses comparison operators to return values related to a value or set of values specified

> **The following are comparison operators**:
>
> | **Operator** | **Description** |
> | --- | --- |
> | `=` | Equal to |
> | `<>` | Not equal to |
> | `>` | Greater than |
> | `<` | Less than |
> | `>=` | Greater than or equal to |
> | `<=` | Less than or equal to |

- *\<\<\<Continue\>\>\>*
  - Leave spaces between mathematical expressions
  - These operators reference an existing column in the table and compare it to any specified value
  - Form:

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name comparison_operator desired_value;

    - **Note**: if comparing column to more than one value, such as a list of values, need to use the operators IN or NOT IN to indicate membership in the list of values or not

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name IN or NOT IN ('value', 'value', 'value', ... );

  - Ranges of values can replace some comparison operators; for example, `BETWEEN` will return values within the specified limits (inclusive) and `NOT BETWEEN` will return all values outside specified range of values

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name BETWEEN or NOT BETWEEN value_1 AND value_2;

  - **Note**: only works for select data types, like numeric values or some date/time values
  - `LIKE` operator will compare strings using "wildcards" to pull from records

> **Wildcards**:
>
> | **Wildcard** | **Description** |
> | --- | --- |
> | `%` | Matches any number of characters |
> | `_` | Matches any single character |
> | `\` | Escapes, will allow consideration of wildcard object as text |

- *\<\<\<Continue\>\>\>*
  - Example: - *generic similarity to any wildcard*

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name LIKE text

  - Example: - *containing "text" anywhere in the text*

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name LIKE %text%

  - Example: - *exactly 1 character before and exactly two characters after "text" in the text*

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name LIKE _text__

  - Example: - *has "n%" at the end of the text*

          SELECT column_name [or *]
          FROM table_name
          WHERE column_name LIKE %n\%

  - **Boolean operators**: `AND` & `OR`; used to customize the conditions in the WHERE clause
    - `AND` returns results when all conditions are true
    - `OR` returns results when any conditions are true
    - `AND` is programmatically processed before `OR`
  - Can query null-valued records by using `IS [NOT] NULL` with WHERE conditional operator
  
> *Can use **mathematical expressions** when querying records*:
>
> | **Expression** | **Description** |
> | --- | --- |
> | `+` | Addition; returns original column value plus specified value |
> | `-` | Subtraction; returns original column value minus specified value |
> | `*` | Multiplication; returns original column value times specified value |
> | `/` | Division; returns original column value divided by specified value |

- *\<\<\<Continue\>\>\>*
  - Can display any new column as a result of an operation as its own alias column name with `AS` operator
  - Example:

          SELECT column_name_1, column_name_2, column_name_2 + [or - or * or /] number_or_formula AS new_name
          FROM table_name;

  - For aliases, can give tables a quick alias name just for context of the query (not to  appear in the results) by writing small string of 1-2 letters after first appearance of table name in the query; then can simply write table_alias.column_name to choose a column from the table whose alias is referenced; very useful for long-winded join queries
    - Example:

          SELECT column_name 
          FROM table_name table_alias ... [more query definition];

- `GROUP BY` - indicates categorization of results
  - Categorizes results using aggregate functions; always use GROUP BY when using a column that is not aggregated with a column that is aggregated

> **Aggregate functions**:
>
> | **Function** | **Description** |
> | --- | --- |
> |  `Avg()` | Returns average value of column parameter passed |
> |  `Count()` | Returns number of rows with values in column parameter passed |
> |  `Max()` | Returns largest value of column parameter passed |
> |  `Min()` | Returns smallest value of column parameter passed |
> |  `Sum()` | Returns sum of values of column parameter passed |
> |  `Mod()` | Performs modular arithmetic on column parameter passed |

- *\<\<\<Continue\>\>\>*
  - Looks like:

          SELECT [column_name,] aggregate_function(column_name [or *])
          FROM table_name 
          [WHERE conditional_statement] 
          GROUP BY column_name;

- `HAVING` - specifies conditions under which category/group will be included in the result of the query (strictly used with GROUP BY)
  - Like a `WHERE` conditional operator, but only for grouped columns
  - Returns grouped results that meet specific criteria
  - Example:

          SELECT [column_name,] aggregate_function(column_name [or *])
          FROM table_name
          [WHERE conditional_statement]
          GROUP BY column_name
          HAVING conditional_statement;

- `ORDER BY` - sorts results according to specific criteria
  - Sorts records by a column or multiple columns
  - *Can give a further ordering to sorted columns*:
    - `ASC` --- Returns results in ascending order (this is the default)
    - `DESC` --- Returns results in descending order
  - `LIMIT` will put a cap on the number of rows returned
  - Example:

          SELECT column_name [or *]
          FROM table_name
          [WHERE conditional_statement]
          ORDER BY column_name
          LIMIT positive integer;

## Other functions

---

- **Scalar functions**: - `pass a column/field as parameter`

> | **Function** | **Description** |
> | --- | --- |
> | `Upper()` | Converts field to upper case letters |
> | `Lower()` | Converts field to lower case letters |
> | `Length()` | Returns length of a text field |
> | `Mid()` | Returns string that matches specified positions |
> | `Round()` | Rounds numeric field to number of decimals specified |
> | `Trim()` | Removes leading & trailing spaces from a string |

- **Date functions**: - `pass a column/field as parameter`

> | **Function** | **Description** |
> | --- | --- |
> `Now()` --- Returns current system date and time
> `Curdate()` --- Returns current system date
> `Curtime()` --- Returns current system time
> `Date()` --- Extracts date part of a date or date/time function
> `Str_to_date()` --- Converts date to recognized format
> `TO_DAYS()` -- Yields the number of days in a given time interval/between two dates
