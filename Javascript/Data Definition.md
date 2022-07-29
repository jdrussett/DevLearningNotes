# Data Definition

## Variable Definition

---

- `var` defines most common variable in Javascript
  - Can be reassigned but only accessed within a function
  - Variables defined with `var` move to top when code is executed
    - Example: ``var `[variable name]` =`[ variable value]` ``
      - `= ""` will declare an empty string
      - `= 0` will declare an empty numeric value
- `const` defines variable that cannot be reassigned
  - Not accessible before it appears within the code
- `let` defines variable similar to const
  - Can be reassigned, cannot be re-declared
- To define a new numeric variable out of a string variable, use a plus sign in the definition
  - Example: `` `[numeric_var]` = + `[string_var]` ``
- `` `[variable_name]` += `[number or string]` `` will add a number or string (whatever specified to the right of `+=`) to the variable, compounding it each time the variable iterates (used within a loop)

## Data Types

---

*Different data types in JavaScript:*

| **Data Type** | **Example** |
| --- | --- |
| **Integer** | `var age = 23;` |
| **Variable** (generic) | `var x;` |
| **Text/string** | `var a = "this is a string";` |
| **Operations** | `var b = 1 + 2 + 3;` |
| **True/false statements** (boolean) | `var c = true;` |
| **Contsant numbers** | `const pi = 3.141592653589793;` |
| **Objects** (like a dictionary in Python, idk) | `var person = {firstName:"John",lastName:"Connor",age:20,nationality:"Dutch"};` |
| **Array** | Generic container for elements of given data type |

### Strings

#### Escape Characters

- `\'` inserts a single quote
- `\"` inserts a double quote
- `\\` inserts a backslash
- `\b` backspaces
- `\f` form feed
- `\n` returns; new line
- `\r` carriage return
- `\t` horizontal tabulator
- `\v` vertical tabulator

#### String Methods

- Use a method on an array by appending it to the end of the string variable name with *dot notation*:

| **String Method** | **Description** |
| --- | --- |
| `.charAt()` | Returns character at a specified position inside a string |
| `.charCodeAt()` | Gives unicode of character at that position |
| `.concat()` | Concatenates two or more strings into one |
| `.fromCharCode()` | Returns a string created from specified sequence of UTF-16 code units |
| `.indexOf()` | Provides position of first occurrence of specified text within a string |
| `.lastIndexOf()` | Same as `indexOf()` but with last occurrence, searching backwards |
| `.length()` | Gets the number of characters in the string |
| `.match()` | Retrieves matches of a string against a search pattern |
| `.replace()` | Find and replace specified text in a string |
| `.search()` | Executes a search for a matching text and returns its position |
| `.slice()` | Extracts a section of a string and returns it as a new string |
| `.split()` | Splits a string into an array of strings at specified position |
| `.substr()` | Similar to `slice()` but extracts a substring depending on a specified number of characters |
| `.substring()` | Also similar to `slice()` and `substr()` but can't accept negative indices |
| `.toLowerCase()` | Convert strings to lower case |
| `.toUpperCase()` | Convert strings to upper case |
| `.valueOf()` | Returns primitive value (that has no properties or methods) of a string |

- `` `[string_name]`.substring(`[number1]`, `[number2]`)`` will return the characters in a string specified by the two numbers
  - Includes the first number but does not include the second number
  - Example:

        var Matt = "Straetker";
        Matt.substring(0,6);

  - will return `"Straet"`
  - `Matt[0:5]` would have returned `"Straet"` as well
- `` `[string_name]`.slice(`[startpoint]`, `[endpoint]`)`` will return the characters from a specified start and end of a string
  - Again, will include first index number but *not* the second one
  - Not specifying an end will cause the count to continue through the entire rest of the string
  - If the entered number is negative, it will count the characters backwards starting at the end of the string
  - Example:

        var dinner = "Chicken Tortellini Alfredo"
        dinner.slice(0,7) == "Chicken"
        dinner.slice(8) == "Tortellini Alfredo"
        dinner.slice(-7) == "Alfredo"

### Arrays

- `[]` defines array in Javascript
  - Example: `var fruits = ["apple", "banana", "orange"];`
  - Populate array with elements that can be strings, integers, other arrays, etc.
  - Blank array can be declared as `var arrayname = [];`
  - Indexing begins at 0 in JavaScript
- Get the *i*th element with bracket notation; i.e. `array_name[i]`
- `` `[array_name]`.length`` gets the length of an array

#### Array Methods

- Use a method on an array by appending it to the end of the array variable name with *dot notation*

| **Array methods** | Description |
| --- | --- |
| `.concat()` | Joins several arrays into one |
| `.indexOf()` | Returns primitive value of specified object |
| `.join()` | Combines elements of an array into a single string and returns the string |
| `.lastIndexOf()` | Gives last position at which a given element appears in an array |
| `.pop()` | Remoes last element of an arry |
| `.push()` | Adds new element at the end of an array |
| `.reverse()` | Sort elements of an array in descending order |
| `.shift()` | Removes first element of an array |
| `.slice()` | Pulls a copy of a portion of an array into a new array |
| `.sort()` | Sorts elements of an array alphabetically, numerically, etc. |
| `.splice()` | Adds element in a specifed way/position |
| `.toString()` | Converts array elements to strings |
| `.unshift()` | Adds a new element to the beginning |
| `.valueOf()` | Returns the first position at which a given element appears in an array |

- Can use multiple methods on one array at the same time
  - Example: `` `[array_name]`.sort().reverse()``

### Dates

#### Setting Dates

- `date()` creates new date object with current date and time
  - Can surround date in quotes, will declare it as a string
    - Example: `date("2020-07-27")`
  - Can create custom date object by passing in seven parameters; year, month, day, hour, minute, second, millisecond
    - Example: `date(2020, 7, 27, 11, 35, 0, 0)`
    - Can omit any of the parameters except year and month

#### Pulling Date/Time Values

- `getDate()` gets day of the month as a number, 1-31
- `getDay()` gets weekday as a number, 0-6
- `getFullYear()` gets year as a four digit number
- `getHours()` gets the hour in a 24-hour clock format, 0-23
- `getMilliseconds()` gets the millisecond value, 0-999
- `getMinutes()` gets the minute, 0-59
- `getMonth()` gets the month, 0-11
- `getSeconds()` gets the second, 0-59
- `getTime()` gets the milliseconds since January 1, 1970
- `getUTCDate()` gets the date of the month in the specified date according to universal time (also available for day, month, fullyear, hours, minutes, etc.)
- `parse()` parses a string representation of a date, and returns the number of milliseconds since January 1, 1970

#### Setting Part of a Date

- `setDate()` sets day of the month as a number, 1-31
- `setFullYear()` sets year as a four digit number
- `setHours()` sets the hour in a 24-hour clock format, 0-23
- `setMilliseconds()` sets the millisecond value, 0-999
- `setMinutes()` sets the minute, 0-59
- `setMonth()` sets the month, 0-11
- `setSeconds()` sets the second, 0-59
- `setTime()` sets the milliseconds since January 1, 1970
- `setUTCDate()` sets the date of the month in the specified date according to universal time (also available for day, month, fullyear, hours, minutes, etc.)
