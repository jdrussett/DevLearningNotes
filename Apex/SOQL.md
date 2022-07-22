# SOQL

## General

---

SOQL stands for "Salesforce Object Query Language"

- Can pass a SOQL statement inside square brackets to dynamically create a list/collection of records resulting from the SOQL query
  - Example:

        Contact[] SmithContacts = [SELECT Id FROM Contact WHERE LastName='Smith'];
  - Referred to as "inline SOQL"

*Basic syntax of any SOQL query*:

    Select [fields] From [object_name] Where [optional_conditional_filters];

> Separate fields, if multiple, with commas
>
> Separate conditions, if multiple, with boolean operators
>> can use parentheses to use nested operators as well

- No `Select *` option in SOQL to select all fields from an object; have to specify each field you want to query explicitly
- Don't need to specify ID field in any SOQL query; always returned automatically with any SOQL query
- SOQL supports wildcard characters with the LIKE operator in queries
  - `%` wildcard matches any or no additional characters in a string
  - `_` wildcard matches exactly one character in a string
  - Example:

        Select name From Account Where name Like 'SFDC%';
        Select email_address__c From Contact Where email_address__c Like '%@fnni.com';

SOQL supports `Order By` sorting mechanism for query results

- Can sort results in ascending or descending order by passing `Asc` or `Desc`
- Can't sort on some field types, like rich text and multi-select picklists
- Can add `Nulls Last` or `Nulls First` to determine if null values on the field sorting by should be ordered first or last

Can limit number of results returned from any query by passing a ``Limit `[positive_integer]` `` parameter

SOQL statements can reference variables declared in Apex code if they are preceded by a colon `:`

- Use of local variable within SOQL statement is called **variable binding**
- Example:

        Integer amountVar = 1000;
        List<Opportunity> oppList = [Select name, amount From Opportunity Where amount >= :amountVar];

*Can query related records in SOQL*:

- To get child records related to a parent record, add an *inner query* for the child records, surrounded by parentheses
- Example:

        SELECT Name, (SELECT LastName FROM Contacts) FROM Account WHERE Name = 'SFDC Computing';

- Queried object on inner-/sub-query **must be pluralized**
- The `From` clause in the nested query references the *relationship* to the child object; for standard objects, this is often simply the object name, but for custom objects, relationship names end in `__r`
- Filter of main query can also be a subquery

Traverse a relationship from a child object to a field on its parent with dot notation

- E.g. if querying on contact object, can get the account name with `Account.Name`

Can use a SOQL query as the container of iteration in a loop statement

- Example:

        for ([variable] : [SOQL query]) {
            ...code to execute...
        }

- Iterative looping variable must be of same type as sObjects being returned from SOQL query

SOQL query *always* returns a type of sObject; to get a different type of object from it, like a list of Ids, can use dot notation on the end of the SOQL query to extract the field you want to create a collection of data type of that field

- Example:

        List<Id> queriedIds = [Select Id From Account Order By Name Asc Limit 20].Id;

Output data type of *every* SOQL query is a list

Aggregate functions for SOQL queries:

- `COUNT()`
- `COUNT_DISTINCT()`
- `MIN()`
- `MAX()`
- `AVG()`
- `SUM()`

> - `GROUP BY` clause determines how other fields are grouped that aren't subject to an aggregate function in the query
> - `HAVING` clause filters results returned from an aggregate function
