# Triggers

## General

---

Apex triggers allow you to perform custom actions before or after events involving Salesforce records

- Can call custom Apex classes, SOQL, or DML with Apex triggers
- Triggers are active by default when created

*Trigger syntax*:

    trigger [trigger_name] on [object_name_of_trigger] ([trigger_events]) {
       … code to execute …
    }

- Each trigger happens on a particular object in Salesforce
- Can specify one or multiple trigger events, comma-delimited, in parentheses
  - Possible events are:
    - `Before insert`
    - `Before update`
    - `Before delete`
    - `After insert`
    - `After update`
    - `After delete`
    - `After undelete`

> **Before triggers** used to update/validate record values before they're saved to the database
>
> **After triggers** used to access field values generated by Salesforce - e.g. Id, `LastModifiedDate`, etc. - and to affect changes in other records

**Context variables** are used to access the records that caused the trigger to fire

- `Trigger.New` contains all records that were inserted in an insert or update trigger
- `Trigger.Old` provides the old version of the sObjects before they were updated by update triggers, or a list of deleted sObjects by a delete trigger
- Some other context variables return Boolean value indicating whether the trigger was fired due to an update, insert, etc.
  - Example: `Trigger.isInsert`
    > Useful when triggers utilize multiple event types!

**Comprehensive list of all context variables available for triggers**:

| **Context variable name** | **Usage/Description** |
| --- | --- |
| `isExecuting` | Returns true if the current context for the Apex code is a trigger (not a Visualforce page, web service, or execute anonymous API call) |
| `isInsert` | Returns true if the trigger was fired due to an insert operation from the Salesforce interface, Apex, or the API |
| `isUpdate` | Returns true if the trigger was fired due to an update operation from the Salesforce interface, Apex, or the API |
| `isDelete` | Returns true if the trigger was fired due to a delete operation from the Salesforce interface, Apex, or the API |
| `isBefore` | Returns true if the trigger was fired before any record was saved |
| `isAfter` | Returns true if the trigger was fired after all records were saved |
| `isUndelete` | Returns true if the trigger was fired after a record was recovered from the Recycle Bin; recovery can occur after undelete operation from Salesforce user interface, Apex, or API |
| `new` | Returns a list of the new versions of the sObject records; this sObject list is only available in insert, update, & undelete triggers, & the records can only be modified in before triggers |
| `newMap` | Map of IDs to the new versions of the sObject records; this map is only available in before update, after insert, after update, & after undelete triggers |
| `old` | Returns a list of the old versions of the sObject records; this sObject list is only available in update & delete triggers |
| `oldMap` | Map of IDs to the old versions of the sObject records; this map is only available in update & delete triggers |
| `operationType` | Returns an enum of type `System.TriggerOperation` corresponding to the current operation; possible values of the `System.TriggerOperation` enum are `BEFORE_INSERT`, `BEFORE_UPDATE`, `BEFORE_DELETE`, `AFTER_INSERT`, `AFTER_UPDATE`, `AFTER_DELETE`, & `AFTER_UNDELETE`; if you vary your programming logic based on different trigger types, consider using the switch statement with different permutations of unique trigger execution enum states |
| `size` | Total number of records in a trigger invocation, `old` and `new` |

> Important note: `trigger.old` and `trigger.new` return lists of sObject records, but when binding them as a filtering condition in a SOQL query, Salesforce automatically converts them to a list of Ids because it's fucking brilliant

Sometimes, restrictions should be added on certain database operations if certain conditions are met, such as preventing records from saving

- `.addError()` method on an sObject will prevent saving records of that object type in a trigger
  - throws a fatal error inside a trigger
  - Calling `.addError()` in a trigger causes entire set of operations to roll back except when bulk DML is called with partial success enabled

For Bulk Apex Triggers, best practice is always to *leave SOQL queries/DML statements outside of any loops* that may be used to retrieve/update records, etc.

- Example, how ***NOT*** to perform SOQL query on bulk Apex trigger:

        trigger SoqlTriggerNotBulk on Account(after update) {
           for (Account a : Trigger.New) {
              Opportunity[] opps = [Select Id, Name, CloseDate From Opportunity Where AccountId = :a.Id];
           }
        }

> Notice how the SOQL query is inside the loop
>
> - **bad...** will result in maxing out SOQL query limits

- Example, how to ***correctly*** perform SOQL query on bulk Apex trigger:

        trigger SoqlTriggerBulk on Account(after update) {
           List<Account> acctsWithOpps = [Select Id, (Select Id, Name, Close From Opportunities) From Account Where Id In :Trigger.New];
           for (Account a : acctsWithOpps) {
              Opportunity[] relatedOpps = a.Opportunities;
           }
        }

> Only one SOQL query, outside of loop
>
> - **good**!

- Similarly, *never* call a DML statement inside a for loop

Triggers execute on batches of 200 records at a time
