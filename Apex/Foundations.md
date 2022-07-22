# Foundations

## General

---

Instantiating objects like lists have to be done on some Salesforce object, like `Account[] acctlist`

- Equally could do `List<Account> acctlist`; nested object types (i.e. a list of accounts, a set of lists, etc.) can be declared in varying order

Access fields on objects with dot notation

- Example: `account_variable.Name__c`

Can loop through a list by creating temporary container variable on an object (i.e. for `(Account acct : acctlist){}`)

- i.e. `list_variable.add(new_element)`, `string_variable.length()`, etc.

> Apex is case-insensitive!
> Apex supports methods on objects, like JavaScript

Apex code can *only be written from scratch in a sandbox org*, not in a production org

- Must be deployed to production from a sandbox

Basic syntax for any class definition is:

    private | public | global [virtual | abstract | with sharing | without sharing] class className [implements interfaceNameList] [extends className] {
       … code to execute; methods …
    }

## Operators

---

| **Operator Name** | **Operator function** |
|---|---|
| ++ | increment operator |
| -- | decrement operator |
| == | equality operator *(Performs case-insensitive string comparisons)* |

## Database Class

---

Apex contains built-in Database class, providing methods that perform DML operations & mirror DML statement counterparts

Available static Database methods that are called on class name:

- `Database.insert()`
- `Database.update()`
- `Database.upsert()`
- `Database.delete()`
- `Database.undelete()`
- `Database.merge()`

Database methods have optional `allOrNone` parameter that allows you to specify whether operation should partially or wholly succeed

- Set to **true** by default
- If set to **false**, if errors occur on partial set of records, successful records will be committed & errors will be returned for failed, non-committed records
  - no exceptions are thrown with partial success route
  - Example:

        Database.insert([record_collection_var], false);

  - The above example implements the `allOrNone` parameter to **false** to allow partial success

Database methods return result objects containing success/failure information for each record

- E.g. insert & update operations return array of `Database.SaveResult` objects
- Example:

        Database.SaveResult[] results = Database.insert([record_collection_var], false);

- Upsert returns `Database.UpsertResult` array of result objects, delete returns `Database.DeleteResult` array of result objects

Database class methods to interact with the results of a database operation:

- `.isSuccess()` method on a database class result list will return only records in the list that succeeded in the operation
- `.getId()` method gets IDs of records in a database class result list
- `.getErrors()` method gets errors of failed records in a database class result list
