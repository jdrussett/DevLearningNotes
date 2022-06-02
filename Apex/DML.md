# DML

## General

---

6 DML operations:

- `insert`
- `update`
- `upsert`
- `delete`
- `undelete`
- `merge`

DML: "**Data Manipulation Language**"

- Provides simple statements to insert, update, merge, delete, & restore records
- `insert` inserts a record or collection of records into their respective object in Salesforce
  - ID field is auto-assigned for each record\* upon an insert statement

> \* ID value is persisted in the database AND is populated on the sObject variable used to insert

- `upsert` creates new records and updates sObject records within a single statement
  - Uses specified field to determine the presence of existing objects
  - Uses Salesforce ID field by default if none is specified
- `merge` merges up to three records of the same sObject type into one of the records, deleting the others, & re-parenting any related records
- `delete` deletes persisted records
  - deletion isn't permanent immediately, records still remain on the Lightning Platform in the Recycle Bin for 15 days and can be restored/recovered
  - Supports cascading deletions for related child records
  - E.g. deleting an account will delete all associated children

Use *Bulk DML* to perform operations on many records at one time by using a DML statement on a collection of objects

- **Limit of 150 DML statements** per Apex transaction!

> If a DML operation fails, it returns an exception of type `DmlException`
>> Catch exceptions in code to handle error conditions

Fields on related records can't be updated with same call to DML operation; this requires a separate DML call

- i.e. updating a contact, or fields on a contact, related to an account, or vice versa

## DML vs. Database Methods?

---

**Use DML statements** if you want any error that occurs during bulk DML processing to be thrown as an Apex exception that immediately interrupts control flow

- By using `try ... catch ...` blocks

        try {
            ... code to try ...
        } catch (`Exception_type` `exception object nickname`) {
            ... code to run in the event of an exception
        }

> This behavior is similar to the way exceptions are handled in most database procedural languages

**Use Database class methods** if you want to allow partial success of a bulk DML operation

- If a record fails, the remainder of the DML operation can still succeed
- Your application can then inspect the rejected records and possibly retry the operation
  - When using this form, you can write code that never throws DML exception errors
    - Instead, your code can use the appropriate results array to judge success or failure

    > **Note**: Database methods also include a syntax that supports thrown exceptions, similar to DML statements
