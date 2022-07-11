# SOSL

## General

---

SOSL stands for "Salesforce Object Search Language"

SOSL is a search language used to perform text searches in records

- Use to search fields across multiple standard & custom object records in Salesforce

Can embed SOSL queries in Apex code just like you can SOQL

- Example: SOSL query that searches for accounts and contacts that have any fields with the word 'SFDC'

        List<List<SObject>> searchList = [FIND 'SFDC' IN ALL FIELDS RETURNING Account(Name), Contact(FirstName,LastName)];

**SOSL can query all objects in Salesforce at once!**

SOSL matches fields based on word match

In Query Editor & the API, search query in SOSL must be surrounded by curly braces, but in Apex code it is surrounded by single quotes

*Can specify the following in each SOSL search query*:

- Text expression - single word or phrase - to search for
- Scope of fields to search
- List of objects & fields to retrieve
- Conditions for selecting rows in source objects

Basic syntax:

- In Apex:

        Find '[search_query_word_or_phrase]' In [search_group] Returning [objects_&_fields]

- In Query Editor, API:

        Find [search_query_word_or_phrase] In [search_group] Returning [objects_&_fields]

Search terms can be grouped with logical operators & parentheses and can include wildcard characters

- `*` wildcard character matches zero or more characters at the middle or end of a search term
- `?` wildcard character matches exactly one character at the middle or end of a search term

Text searches in SOSL are case-insensitive

Adding search group parameter with `In` in a query is optional; if left out the default will be all fields; can specify one of the following values:

- All Fields
- Name Fields
- Email Fields
- Phone Fields
- Sidebar Fields

Objects & fields parameter is also optional in SOSL queries; specifies information to return in a search result: list of one or more sObjects with each one or more fields, with optional values to filter against

> If not specified, default is to return IDs of all object records found

The search query parameter can take on one of two types: single word(s) or phrase

- *Single word(s)* are delimited by spaces, punctuation, and changes between letters and digits; surrounded by *single quotes*
- *Phrases* are a collection of words and spaces, surrounded in *double quotes*; multiple words can optionally be combined together with logic/grouping operators to form more complex query

Can add `Order By`, `Where` conditional clauses, or `Limit` statements to the objects & fields parameter portion of the query

- Example:

        Find 'Steel' In All Fields Returning Account(Name, Industry Where Industry = 'Manufacturing'), Contact(Name, Phone);
