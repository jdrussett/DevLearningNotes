# Data Definition

## General

---

Can declare collections (lists) of objects either with nested data type notation or with array notation

> Example: the following statements are equivalent
>
>     List<String> list_name = new List<String>();
>     String[] list_name = new List<String>();

- To preemptively declare/restrict the size of a list, can specify the length of the list in bracket notation
  - Example: `String[] stringListOfLength4 = new String[4]`

Create a new collection or sObject dynamically with curly brackets

- Example: `List<String> colors = new List<String> {'red', 'green', 'blue'};`

You **must** declare each new variable proceeding a data type for that variable, **always**

> Examples:
>
>     Integer i;
>     String name;
>     Double ratio;
>     ... etc. ...

Can declare new sObject with fields populated dynamically by passing field value-pairs inside parentheses

> Example:
>
>     Account acc = new Account(
>       name = 'New Account Name',
>       phone = '612-423-5635',
>       address = '1005 N 20th St APT 425'
>     );

- Can also access/define sObject fields with dot notation

## Supported Data Types in Apex

---

### Primitive Data Types

- Integer
- Double
- Long
- Date
- Datetime
- String
- Boolean
- ID

### sObject Data Type

> This is any data type in Apex that represents a record of a standard or custom object type in Salesforce

- i.e. an `Account` sObject, or a `Candidate__c` object

Generic sObject type can reference any record in salesforce

- Can be created only through `newSObject()` method
- Fields can be accessed only via `put()` and `get()` methods

### Collection Data Types

| **Collection Data Type** | **Valid element data types** |
| --- | --- |
| List | primitives, sObjects, or other collections |
| Set | primitives |
| Map | primitive to another primitive, to an sObject, or to a collection |

> A set is an unordered collection of elements that does not allow duplicate values

A **map** is a collection of key-value pairs where each unique key maps to a single value

- Keys/values can be any data type and can contain any collection as well as nested collections
  - i.e. can have a map of integers to maps, which map strings to lists, ... etc.
  - Keys can contain up to 4 levels of nested collections
- You can define a map of IDs to sObjects with a SOQL statement such as: 

      Map<Id, Account> TargetAccountsMap = new Map<Id, Account>(
        [SELECT Id, Total_Transfers_In__c, Total_Transfers_Out__c, Total_Card_Charges__c, Type
        FROM Account
        WHERE Id IN :TargetAccountIds]
      );

- More help on maps: [https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/langCon_apex_collections_maps.htm](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/langCon_apex_collections_maps.htm)

### Other Data Types

- Enum, or a typed list of values  
- User-defined apex classes  
- System-supplied apex classes  

## JSON

---

Built-in `JSONParser` class converts JSON input into an object

- Useful tool to convert JSON payloads to Apex can be found at the [JSON2Apex](https://json2apex.herokuapp.com/) tool
