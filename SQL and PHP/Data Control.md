# Data Control

**Data Control Language**: commands that control a database, including administration privileges

- Can create new database (or SCHEMA) using the `CREATE` command
- Conditional statement `IF NOT EXISTS` can be added to query to only create database by chosen name if one of that name doesn't currently exist
  - Example:

          CREATE SCHEMA [IF NOT EXISTS] database_name;

    - Like a table, schema can also be dropped using `DROP` command
- Can also create new users to a database with username & password; password designated with the command `IDENTIFIED BY`
  - Example:

          CREATE USER 'user_name' IDENTIFIED BY 'user_password';

- `GRANT` command bestows privileges of interaction with the database to a designated user(s)
  - Example:

          GRANT privilege(s) ON database_name.table_name 
          TO user_name;

> *List of all privileges that can be granted:*
>
> | **Privilege Name** | **Description** |
> | --- | --- |
> | `ALL` | All privileges (below) |
> | `CREATE` | Ability to create tables |
> | `SELECT` | Ability to perform select statements on table/view |
> | `INSERT` | Ability to perform insert statements on table/view |
> | `UPDATE` | Ability to perform update statements on table/view |
> | `DELETE` | Ability to perform delete statements on table/view |
> | `REFERENCES` | Ability to create foreign key constraint to refer to another table |
> | `ALTER` | Ability to perform alter table statements to change table definition |
> | `DROP` | Ability to drop objects in database |

- *\<\<\<Continue\>\>\>*
  - `WITH GRANT OPTION` allows any user granted privileges to in turn grant any of the privileges granted to them to another user
    - Example:

          GRANT privilege(s) ON database_name.table_name 
          TO user_name WITH GRANT OPTION;

  - Revoking privileges is done in same format as granting them using `REVOKE` command; operator `FROM` must be used instead of `TO`
    - **Note**: if also revoking grant option from a user as well, must be done separately from revocation of privileges
    - Example:

          REVOKE privilege(s) ON database_name.table_name FROM user_name;
          REVOKE GRANT OPTION ON database_name.table_name FROM user_name;
