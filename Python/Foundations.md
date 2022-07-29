# Foundations

## Foundational Essentials

---

- `Print()` function displays variables/expression values to the console; similar to `console.log` in Javascript or `system.debug` in Apex
  - Can pass multiple parameters, separated by commas
  - Parameter end='' will write next print output on the same line, delimited by what is contained in the '' of the end parameter
- Comment out a line in Python with `#`
- Multi-line comments in Python with triple quotes (can be double or single)
  - Example:

        ''' this text would all be commented out, even if it spanned multiple lines '''

- `\n` for a new line, same as in Javascript

- Modules available for in other modules and scripts using `import` command
  - Example: `'import math'` will import the math module
  - Use dot notation to access objects
- Methods executed in Python with method name following a "`.`" and an object
  - Example: to add a new element to a list (using append method below), use `` `list_name`.append(`new_list_element`)``

## Defining Data

---

- `Input()` function collects user input, stores into variable as declared with type of string
  - Adding string parameter to input() function will display text before presenting user with input text box
- `Int()` function converts a string to an integer
- `Str()` function returns an object's value in string form
- `Float()` allows for continuous numerical data
  - As in you could move ("float") the decimal place to any point in the value and it would still make sense in theory
  - For continuous, not discrete, data
  - Float type numeric data can be represented with scientific notation, appending the letter 'e' to the end of a number and then the power you want to raise 10 to and multiply the number by
    - Example:

        47,917,636 == 4.7917e7

- `type()` function will print the type of an object
- `id()` function will print the id/memory address of an object
- `map()` function takes two arguments; first item is a data type, second argument is a given value/object that you want to convert to that data type
  - Works well with a loop/converting each element of a container to a different data format

## Basic Functions/Operators

---

- **Equality operator** evaluates to true if the left and ride side of its input are equal
  - Example: `num_people = 10; num_people == 10;` evaluates to `TRUE`
- **Relational operators** include `>`, `<`, `>=`, `<=`
  - Can chain operators with Python
  - Example:

        if 0 < num_people <= 10: print('Ten people or less')

- **Membership operators** evalute whether the left-side operand is equal to an element of the right-hand operand
  - If `x` is a tuple or list, then `a in x` evaluates to `TRUE` if there is an index `i` in `x` for which `a == x[i]`
  - Operators are `in` and `not in`
- **Identity operators** are used to determine whether two objects given are the same or not
  - Operators are `is` and `is not`
- `id()` function used to retrieve identifier of any object
- `Len()` function used to get the length/count of characters of any string or other sequence object type
  - Using a `\` after a string literal will extend the string to the next line
- `Range()` function generates `x` many integers from `0` to `(x-1)`
  - Can also use to specify finite number of loops to complete
  - Example:

            for `index variable` in range(`x`)

- Can use `reversed()` function to iterate over the elements in a container going backwards (start with the last element, end with the first)
  - Example:

            for `index variable` in reversed(`container`):
