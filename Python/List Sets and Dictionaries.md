# Lists Sets and Dictionaries

## Lists

---

Lists are created with brackets in Python as they are in JavaScript

- Elements maintain positional ordering
- Can update individual index values/elements of a list using bracket notation

Use negative indices to obtain values from a list starting at the end

- Example:

        my_list = [1, 2, 3, 4, 5]
        my_list[-1] == 5

Can also create list with `list()` function; takes single iterable object argument (`string`, `list`, `tuple`) to create new list delimited by whatever characters passed

- Example:

        list('abc') = ['a', 'b', 'c']

Method `append()` adds new elements to a list

Method `extend()` adds all items in container passed to the list the method references

- Another way to add two lists together, etc.

Method `pop()` or `remove()` removes elements from a list

- `Pop` removes based on index specified, `remove` removes based on literal value specified

Some helpful sequence-type functions and methods include:

| **Function/Method Name** | **Function/Method Description**
| --- | --- |
| ``Len(`list`)`` | Find the length of a list |
| `` `list1` + `list2` `` | Produce a new list by concatenating two existing lists |
| ``All(`list`)`` | Returns `True` if a list is empty or contains no elements equal to 0 |
| ``Any(`list`)`` | Returns `True` if a list contains any element not equal to 0 |
| ``Min(`list`)`` | Find the element in the list with the smallest value |
| ``Max(`list`)`` | Find the element in the list with the largest value |
| `` `list`.sort()`` | Sorts items of list in-place (list has to contain `integer`/`float` values) |
| `` `list`.sorted()`` | Like the `sort` method, but creates/returns new list instead of modifying original list |
| ``Sum(`list`)`` | Find the sum of all the elements in a list (containing only integer/double type data) |
| `` `list`.insert(`i`, `x`)`` | Inserts value `x` into the list before list position `i` |
| `` `list`.index(`given_value`)`` | Find the index of the first element in the list whose value matches the value given |
| `` `list`.count(`given_value`)`` | Find the count of occurrences of the given value element in the list |

`.sort()` and `.sorted()` methods both have optional `key=` argument that can specify a function to apply to each element being sorted before sorting

To sort a list from highest-to-lowest instead of lowest-to-highest, include the argument `reverse=True`

**Tuples** are like lists but declared with parentheses instead of brackets and their elements and their order cannot change

`Enumerate()` function yields new tuple for each iteration of a loop containing both the index and value of a list iterating over

- Use like a for loop, but provide two objects, separated by comma, to provide index and value, respectively
- Example:

        for `index`, `value` in enumerate(`list`):

    > can now work with both index and value for each loop iteration

To create an exact copy/replica of a list (for manipulation purposes, while still maintaining integrity of original list) use **slice notation** on list to create copy of list spanning all of its elements

- Example:

        string_copy = original_string[:]

    > *IMPORTANT NOTE*: if modifying lists/list elements while iterating over that list, iterate over a copy of that list while making changes to original list to preserve loop integrity

Can use slice notation to add elements of one list (or the whole list) to the end of another list

- Slice of a list generates a list
- Example:

        `my_list`[len(`my_list`):] = [`my_other_list`]

- will add elements of my_other_list to end of my_list
  - Substitute option for just adding two lists together with `+`
- Add optional third component, **stride**, to slice notation to indicate length of step from one value to the next
  - Format: `` `my_list`[0:len(`my_list`)-1:2]`` gets *every other element* of `my_list` starting at the first element, element 0

Common list slicing operations:

| **List Slice Operation** | **Description** |
| --- | --- |
| `` `my_list`[`a`:`b`]`` | Get a list from `a` (including `a`) to `b` (not including `b`) of `my_list` |
| `` `my_list`[`a`:`b`:`c`]`` | Get a list from `a` (including `a`) to `b` (not including `b`) of every `c`th item of `my_list` |
| `` `my_list`[`a`:]`` | Get a list from `a` (including `a`) to the end of `my_list` |
| `` `my_list`[:`b`]`` | Get a list from the start of `my_list` to `b` (not including `b`) |
| `` `my_list`[:]`` | Get an exact copy of `my_list` |

`reverse()` method reverses the order of the elements in the list

Two different styles of looping over lists:

- ``For `x` in `list` ``
  - loops over each value in `list` (`x` takes on value of each value in `list` for each iteration)
- ``For `x` in range(len(`list`)):``
  - loops over each index in `list` (`x` takes on value of each index in `list` for each iteration)

**List nesting** refers to a list containing one or more elements that is *also* a list

- Allows creation of multi-dimensional data structures
- Use compound bracket notation to access element of a list nested in another list

**List comprehension** is a convenient construct the Python interpreter provides to iterate over a list, modify the elements of the list in a uniform way, and return a new list containing all the modified elements from the previous list

- Format: `` `new_list` = [`expression` for `name` in `original_list`]``

- Example:

        list1 = [1, 3, 5, 7, 9]
        list2 = [(i*2) for i in list1]
        list2 == [2, 6, 10, 14, 18]

3 components of a list comprehension:

1. **Expression component** - to evaluate for each element in iterable object/original list
2. **Loop variable component** - to bind the current iteration element
3. **Iterable object component** - to iterate over (original list, in this case; could also be a tuple, string, enumerate, etc.)

List comprehensions can be extended with optional conditional statement to filter out some of input list values/elements

- Format: ``new_list = [`expression` for `name` in `original list` if `pre-qualifying conditional expression`]``

## Sets

---

`Set()` function will declare a set

- Example:

        `example_set` = set(['`element1`', '`element2`', '`element3`'])

- Using curly braces also declares a set

  - Example:

        `example_set` = {'`element1`', '`element2`', '`element3`'}

Useful supported methods on sets include:

| **Set Method** | **Description** |
| --- | --- |
| ``Len(`set`)`` | Find length (number of elements) of `set` |
| `` `Set_1`.update(`set_2`)`` | Adds elements of `set_2` to `set_1` |
| `` `set`.add(`value`)`` | Adds `value` as an element of `set` |
| `` `set`.remove(`value`)`` | Removes `value` from `set` if it exists |
| `` `set`.pop()`` | Removes one element at random from `set` |
| `` `set`.clear`` | Clears all elements from `set` |

Python set objects support standard/conventional set theory operations:

| **Standard Set Operation** | **Description** |
| --- | --- |
| `` `set_1`.union(`set_2`, `set_3`, `set_4`, ...)`` | Returns a new set containing all the elements that live in the union of all the sets provided |
| `` `set_1`.intersection(`set_2`, `set_3`, `set_4`, ...)`` | Returns a new set containing only the elements that live in the intersection of all the sets provided |
| `` `set_1`.difference(`set_2`, `set_3`, `set_4`, ...)`` | Returns a new set containing only the elements in `set_1` that are not found in any of the other sets provided |
| `` `set_1`.symmetric_difference(`set_2`)`` | Returns a new set containing only elements that appear in exactly one of either `set_1` or `set_2` |

## Dictionaries

---

**Dictionary** object in Python defined with curly braces surrounding key:value pairs

- Example:

        [dictionary_name] = {[key_1]:[value_1], [key_2]:[value_2], ... }

- Can also create with `dict()` function, as in:

        `dictionary_name` = dict('`key1`'='`value1`', '`key2`'='`value2`')

- or:

        `dictionary_name`=dict([('`key1`', '`value1`'),('`key2`', '`value2`')])

Dictionaries can contain objects of arbitrary type, even other containers (lists, tuples, etc.)

Access a dictionary element by specifying a key in brackets appended to dictionary name

- Example: if `dictionary_1` = `{'key_1':'value_1', 'key_2':'value_2', 'key_3':'value_3'}`, obtain 'value_2' by typing `dictionary_1['key_2']`

Common dictionary operations:

| **Dictionary Operation** | **Description** |
| --- | --- |
| `` `dict_name`[`existing_key`]`` | Get dictionary value associated with `existing_key` |
| `` `dict_name`[`new_key`] = `new_value` `` | Add dictionary element with key of `new_key` and value of `new_value` |
| `` `dict_name`[`existing_key`] = `new_value` `` | Update dictionary value element with key `existing_key` to `new_value` |
| ``del `dict_name`[`existing_key`]`` | Delete existing dictionary element (key and value) with key of `existing_key` |
| `` `test_key` in `dict_name` `` | Tests for existence of key named `test_key` in dictionary `dict_name`; returns boolean value |
| `` `dict_name`.clear()`` | Clear all items from dictionary `dict_name` |
| `` `dict_name`.get(`existing_key`, "else text")`` | Read the associated value of key `existing_key` from dictionary `dict_name`; returns value of `"else text"` if key does not exist in `dict_name` |
| `` `dict_name1`.update(`dict_name2`)`` | Merges two dictionaries by adding elements of `dict_name2` to `dict_name1`; existing entries in `dict_name1` are overwritten if same keys exist in `dict_name2` |
| `` `dict_name`.pop(`existing_key`, `default`)`` | Removes key/value pair from `dict_name` with key of `existing_key`; if key doesn't exist, `default` value is returned |

Remove & return key value from dictionary; if key does not exist, default value `"N/A"` is returned

Can use for loops on dictionaries; key of each dictionary entry is object of iteration

- Order elements added to dictionary **is not equal to** order keys may be iterated through

Python interpreter creates **hash** of each key in a dictionary

- Hash is a transformation of a key into a unique value that allows the interpreter to perform a lookup very quickly

Dictionary type also supports methods `.items()`, `.keys()`, and `.values()`

- each produce a **view object**: provides read-only access to dictionary keys and values
- Program iterates over view object to access one key-value pair/key/value at a time
- View object reflects updates made to a dictionary, even if dictionary is altered after view object is created

| **View Object Generating Dictionary Method** | **Result** |
| --- | --- |
| `` `dict_name`.items()`` | Returns view object that yields key/value tuples from dictionary `dict_name` |
| `` `dict_name`.keys()`` | Returns view object that yields keys from dictionary `dict_name` |
| `` `dict_name`.values()`` | Returns view object that yields values from dictionary `dict_name` |

> Note: these methods produce a single result object, not a container filled with multiple elements of result objects
>
> - To obtain a container of separate result objects, use `list()` function

Dictionary can contain **nested dictionaries** in which dictionary contains another dictionary as one of its values

- Indexing operations applied to nested dictionaries by using consecutive bracket notation
- Code tends to be more readable in nested fashion, visually separated (interpreter ignores whitespaces for multi-line constructs)

Nested dictionaries serve as a powerful **data structure**: method of organizing data into logical & coherent fashion

If a string contains many conversion specifiers ('`%s`', '`%`'), may become difficult to read

- Instead of just using a tuple of substitute values, can use a dictionary to the right of the conversion operator and include a **mapping key** for all conversion specifiers; specified by indicating key of relevant value in dictionary with parentheses
- Example:

        'time: %d:%02d:%d' % (11, 2, 15.002) == '11:02:15.002'

Can be represented more clearly as: 'time: %(hour)d:%(minute)02d:%(second)f' % {'hour' : 11, 'minute' : 2, 'second' : 15.002}
