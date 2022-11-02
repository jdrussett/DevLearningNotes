# Transaction Control

**Transaction Control Language**: commands used to manage changes made by data manipulation statements; allows statements to be grouped together into logical transactions

- `COMMIT` writes changes to database; solidifies all queries in script not yet committed
- `ROLLBACK` restores database to statues since last commit command
- `SAVEPOINT` will tell rollback command to restore to it instead of last commit command
  - In MySQL Workbench, changes will be automatically committed
    - Irreversible using rollback
  - To toggle this function on/off, use the following commands:

          SET autocommit = 0; --this will disable autocommit
          SET autocommit = 1; --this will enable autocommit
