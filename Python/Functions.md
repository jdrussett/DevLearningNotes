# Functions

## Function Basics

---

Use `def` keyword to create new functions in Python

- Example:

        def [function_name]():

Function can return a value using the `return` command

`None` is special keyword that indicates no value/returned value

Statement `raise NotImplementedError` will cause program to stop execution if it runs into this function which has not been finished

> Indicates function is not implemented and causes program to stop execution

`Global` statement must be used in front of a variable name to change its value inside a function if it is a global variable

- Used as its own separate statement; run ``global `variable_name` ``, begin new line, then can begin using variable inside function statements

Function `locals()` examines all variables defined in current local namespace

Function `globals()` examines all variables defined in global namespace

To pass a copy of a list (mutable object) to a function to modify it in the function but not outside the function, can pass a copy with `` `function_name`(`list_name`[:])``

Functions can contain parameters that indicate allowance for **extra arguments** (must come last in function definition)

- `*args` collects optional positional parameters into arbitrary argument list tuple
- `**kwargs` creates dictionary of extra arguments not defined in function definition
