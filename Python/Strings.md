# Strings

## Conversion Specifiers

---

**String formatting expressions** allow creating strings with placeholders that are replaced by values of variables specified elsewhere

- `%s` conversion specifier inserts a string variable
- `%d` conversion specifier inserts an integer variable
- `%f` conversion specifier inserts a float variable
  - Specifying `%0.[x]f` will print exactly `[x]` many digits after the decimal point
  - Example:

        total_people = 75
        dollars =  68
        best_friend = 'Sophie'
        
        Print('Your best friend is %s.' % best_friend)
        Print('You know %d different people.' % total_people)
        Print('You have %f dollars in your pocket.' % dollars)
        
        [[Your best friend is Sophie.]]
        [[You know 75 different people.]]
        [[You have 68.000000 dollars in your pocket.]]

Common conversion specifiers:

| **Conversion Specifier** | **Notes** | **Example** | **Output of Example** |
| --- | --- | --- | --- |
| `%d` | Substitute as integer | `Print('%d' % 10)` | 10 |
| `%d%%` | Substitute a percentage | `Print('%d%%' % 40)` | 40% |
| `%f` | Substitute as floating-point decimal | `Print('%f' % 15.2)` | 15.200000 |
| `%s` | Substitute as string | `Print('%s' % 'ABC')` | ABC |
| `%x, %X` | Substitute as hexadecimal in lowercase (`%x`) or uppercase (`%X`) | `Print('%x' % 31)` | 1f |
| `%e, %E` | Substitute as floating-point exponential format in lowercase (`%e`) or uppercase (`%E`) | `Print('%E' % 16386)` | 1.6386E+04 |

## String Functions

---

- `Split()` function will split a string into many different substrings depending on which delimiting character or expression you pass & create a list of the results
- `Strip()` function returns a copy of the string you pass it with leading and trailing whitespaces removed

## String Methods

---

*String methods* (must be appended to string name after a `.` to be used):

- ``Replace(`old string`, `new string`)`` replaces old substring with new substring within a string
  - Optional third parameter `count` replaces only first predefined number of substrings
- `Find()` searches string for substring passed, returns index of first result found
  - Can optionally add `start`, `end` parameters to limit search
  - Can specify `rfind()` to search string in reverse
- `Count()` returns number of times a passed substring is found in a string

Methods on strings that return Boolean values:

| **Method Name** | **Description** |
| --- | --- |
| `.isalnum()` | Returns true if all characters in string are uppercase or lowercase letters or digits 0-9 |
| `.isdigit()` | Returns true if all characters are digits 0-9 |
| `.islower()` | Returns true if all characters are lowercase letters |
| `.isupper()` | Returns true if all cased characters are uppercase letters |
| `.isspace()` | Returns true if all characters are whitespace |
| `.startswith()` | Returns true if string starts with value passed |
| .endswith() | Returns true if string ends with value passed |

Methods on strings that create strings based on strings inputted:

| **Method Name** | **Description** |
| --- | --- |
| `.capitalize()` | Returns copy of string with first character capitalized & rest lowercase |
| `.lower()` | Returns copy of string with all characters lowercase |
| `.upper()` | Returns copy of string with all characters uppercase |
| `.strip()` | Returns copy of string with all leading & trailing whitespaces removed |
| `.title()` | Returns copy of string with first letters of each word capitalized |
| `.split()` | Returns list of substrings created from given string, delimited by character or sequence of characters passed |
| `.join()` | Returns single string created by concatenation of single list of strings provided and separator character(s) |

## Strings Misc

---

> **Cool note**: if you apply the multiplication operator to a string it will print that string back to back by the number of times you specify
>
> - Example:
>
>        user_value = 'XO'
>        user_value * 5 = XOXOXOXOXO

- Individual string characters read using bracket notation
- Slice notation reads multiple consecutive characters of a string, passing starting and ending index values
  - Ending index not included
  - Example:

            my_string = 'Hello world'
            my_string[4:7] = 'o w'

  - Optional third parameter `stride`: included after colon after ending index, determines width of increment
- If looping over a string, have to use `range(len([string]))` to cause the loop to iterate over each character in the string
