# Working With Data

## General

---

`.add()` method adds elements to a collection after it's been created

- Example:

        List<String> colors = new List<String> {'red', 'green'};
        colors.add('blue');

- Can add index parameter to `.add()` method (integer, placed before item to add to collection) to specify specific index you'd like the list item to have
- Example:

        listOfFruits.add(4, 'pomegranate')

Can get collection elements with bracket notation (``list_variable[`desired_index`]``) or with `.get()` method

> Indexing begins at 0 in Apex
>
> - Example: if variable `colors` is defined as `List<String> colors = new List<String> {'red', 'green', 'blue'}`, then `colors[1]` and `colors.get(1)` will both return `'green'`

`.size()` method returns the size of a collection or the character count of a string, etc.

`.put()` method on a map takes parameters for key and value; adds entries to a map

`.get()` method returns value for a key provided on a map

- If provided key is not mapped to a value, `get()` method returns null

``Date.newInstance(`yyyy`, `mm`, `dd`)`` function will define a date data point in Apex

`Integer.valueOf()` returns the integer value of another data type like a string or a generic object
