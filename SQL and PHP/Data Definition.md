# Data Definition

**Data Definition Language**: interacts with database structures; commands that define a database

- `CREATE`: creates new objects in the database
  - Applies to:
    - Tables
    - Constraints (relationships)
- `ALTER`: allows changing of table/column specifications
  - Paired with any of the following actions:
    - `ADD` adds column to table
    - `CHANGE` changes existing column to new name and conditions specified
    - `DROP` will drop entire table or column or constraint

*Table creation:*

1. Upon creation, specify name of table after `CREATE TABLE`, & separate columns with parentheses; each column separated by a comma; identify data types for each column
   - List of data types include:
      - Text: char(), varchar(), blob(), text
      - Number: tinyint(), smallint(), mediumint(), int(), bigint(), float(), double(), decimal()
      - Date: date(), time(), datetime(), timestamp()
   - Looks like:

          CREATE TABLE table_name (
              column_name data_type()
          );

2. Next, identify columns that can/cannot be null/empty (not null is the default assumption)
   - Looks like:

          CREATE TABLE table_name(
               column_name data_type() NOT NULL
          );

3. Specify whether columns auto-increment; only pertains to numeric columns
   - Looks like:

          CREATE TABLE table_name(
               column_name data_type() [NOT NULL] AUTO_INCREMENT
          );

4. Identify unique column(s), namely primary key
    - Looks like:

          CREATE TABLE table_name(
               column_name data_type() [NOT NULL] [AUTO_INCREMENT] PRIMARY KEY
          );

5. State primary key/foreign key pairs and relational integrity controls; key pairings are done via the creation of a constraint, referencing the foreign key in one table (the table you're working in) to the primary key of another table
    - Looks like:

          CREATE TABLE table_name(
               column_name data_type() [NOT NULL] [AUTO_INCREMENT] CONSTRAINT constraint_name FOREIGN KEY (column_name of current table) REFERENCES other table name (column_name of primary key in other table)
          );

    > - *Note*: the constraint itself is named and created in order to link two other columns (usually just column_name_fk1)

    - **Relational integrity controls**: specifies an action to be done to a row/column given the occurrence of a previous given action; referential integrity enforce via primary key/foreign key matching
    - Preceding commands:
      - `DELETE`
      - `UPDATE`
    - Following commands:
      - `RESTRICT` - does not allow change of independent column/row unless all columns/rows dependent on it are deleted/updated first
      - `CASCADE` - if independent column/row is deleted, all columns/rows linked to it will also be deleted
      - `SET NULL` - foreign key value will be set to null for all columns/rows linked to a deleted/updated independent row/column
      - `SET DEFAULT` - foreign key value will be set to a default value for all columns/rows linked to a deleted/updated independent row/column
    - Looks like:

          CREATE TABLE table_name(
               column_name data_type() [NOT NULL] [AUTO_INCREMENT] CONSTRAINT constraint_name FOREIGN KEY (column_name of current table) REFERENCES other table name (column_name of primary key in other table) ON preceding_command following_command
          );

6. Determine default values; not applicable to all columns/data types, but sometimes useful for times/dates
    - Looks like:

          CREATE TABLE table_name(
               column_name data_type() [NOT NULL] ... DEFAULT [command] value
          );

    - The command could be a keyword like NOW if the data type was date/time

*Layout for creation of a table:*

    CREATE TABLE table_name (
        column_name data_type() [NOT NULL] [AUTO_INCREMENT] [PRIMARY  KEY],
        column_name data_type() [NOT NULL] [AUTO_INCREMENT] [CONSTRAINT constraint_name FOREIGN KEY (current column name) REFERENCES other table name (other table primary key)]
        ...
    );

> Create as many columns as there are in the table, put a comma after all definitions except the last one

- `TRUNCATE` command removes all records from a table; these records are not recoverable
- **Note on SQL syntax**: enters/spaces/capitalizations not always necessary; just used by convention to help remember different field types & for organizational purposes
- **Altering a table** (after creation): use `ALTER TABLE table_name` to begin operation; can then follow with any of table altering commands - `ADD`, `CHANGE`, `DROP` - to make changes to any column or constraint
  - Examples:
    - `ALTER TABLE table_name CHANGE column_name new_column_name new_data_type() [NOT NULL] ... ;`
    - `ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY (column_name) REFERENCES other_table_name (primary_key_of_other_table);`
  - `DROP` command is unique because it can be used to drop column in a table or the whole table itself; if the former, just use it as described above after `ALTER TABLE` statement, but if dropping entire table, do it in one line:

        DROP TABLE table_name
