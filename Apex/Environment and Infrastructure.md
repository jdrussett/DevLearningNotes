# Environment and Infrastructure

## General

---

> An Apex **class** is like a file; contains code in a tangible location
>> An Apex **method** is a section of a class that does something useful

- Method names always have to be followed by `()`, regardless of whether any parameters are passed to the method or not
- Call a method by using dot notation to access the method from the class and optionally passing parameters \(inside `()`\) required
- Each method definition has to include what object that method is expected to return
  - i.e. if a method is supposed to return a list of contacts, have to define it as something like `public static List<Contact> searchForContacts { … }`

> Language constructs supported by Apex:
>
> - Classes, interfaces, properties, collections (arrays)
> - Object & array notation
> - Expressions, variables, constants
> - Conditional statements

Apex allows you to make calls to and integrate Apex code with *external web services*

- Apex calls to external web services referred to as **callouts**
- Call must be asynchronous so trigger process doesn't block you from working while waiting for external web service's response
- To make a callout from a trigger, call a class method that executes asynchronously
  - A **future method** is annotated with `@future(callout=true)`

> Can save up to 6 MB of Apex code in each org (not counting test methods)

## Access Modifiers

---

Different Access modifiers that are available for use:

| **Modifier** | **Description** |
| --- | --- |
| `global` | More permissive than public, allows access across namespaces and applications |
| `public` | |
| `private` | |
| `static` | Easier to call than instance methods, don't need to be called on an instance of the class, and simply called directly on the class name |
| `void` | |

The `with sharing` keyword specifies that sharing rules for the current user *should* be taken into account for an Apex class

- Note, this almost always *restricts* data more than it grants additional visibility

By default, Apex executes in `system context`, meaning the code has access to all objects, fields, and records in the org

- Object permissions, field-level security, sharing rules are *not applied* for the current user by default

## User Interface API

---

### UI API resources

Return data, metadata, & layout information based on record ID(s) passed

- ``/ui-api/record-ui/`[record_IDs]` ``

Can get layout/object metadata/data responses individually

- ``/ui-api/layout/`[object_API_name]` ``
- ``/ui-api/object-info/`[object_API_name]` ``
- ``/ui-api/records/`[record_IDs]` ``

Get default field values needed to build UI for cloning/creating a record

- ``/ui-api/record-defaults/create/`[object_API_name]` ``
- ``/ui-api/record-defaults/clone/`[record_IDs]` ``

Get values for all picklist fields of a specific record type

- ``/ui-api/object-info/`[object_API_name]`/picklist-values/`[record_type_ID]` ``

Get list of records and list view metadata

- ``/ui-api/list-ui/$`[list_view_ID]` ``
- ``/ui-api/list-ui/$`[object_API_name]`/$`[list_view_API_name]` ``
- ``/ui-api/list-info/$`[list_view_ID]` ``
- ``/ui-api/list-info/$`[object_API_name]`/$`[list_view_API_name]` ``
- ``/ui-api/list-records/$`[list_view_ID]` ``
- ``/ui-api/list-records/$`[object_API_name]`/$`[list_view_API_name]` ``

Get list of actions available to the user in the Salesforce app, in global actions header, on record detail & edit pages, on related lists, etc.

- `/ui-api/actions/global`
- ``/ui-api/actions/record/$`[record_IDs]` ``
- ``/ui-api/actions/record/$`[record_ID]`/record-edit``
- ``/ui-api/actions/record/$`[record_ID]`/related-list/$`[related_list_IDs]` ``

Get list of favorites in the header

- `/ui-api/favorites`
- ``/ui-api/favorites/$`[favorite_ID]` ``
- `/ui-api/favorites/batch`
- `/ui-api/favorites/$`[favorite_ID]`/usage`

Get lookups/related records to a record

- ``/ui-api/lookups/`[object_API_name]`/`[field_API_name]` ``
- ``/ui-api/lookups/`[object_API_name]`/`[field_API_name]`/`[target_API_name]` ``
