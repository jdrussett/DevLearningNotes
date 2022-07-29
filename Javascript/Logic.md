# Logic

## Loops

---

*Format:*

    for (before loop iteration; condition for loop; execute after loop) {
        // code to execute during each loop iteration
    }

### Types of Loops

- **for loop** - most common way to create a loop in JavaScript
  - Example:

        for (var i = `initial count`; `condition determining when i stops counting`; i++){
            ... code to execute ...
        }

- **while loop** - sets up conditions under which a loop executes (until conditions are no longer met)
  - Example:

        while (`condition allowing i to continue counting`){
            ... code to execute ...
        }

- **do while loop** - similar to while loop, but executes at least once and performs a check at the end to see if the condition is met to execute again
- Looping tools:
  - `break` - used to stop & exit the cycle at certain conditions
  - `continue` - skip parts of the cycle if certain conditions are met
- Increment a counting variable with `++` operator in the array definition

## If-Else Statements

---

*Format:*

    if (`condition to execute code`) {
        // code to execute if condition evaluates to true
    } else {
        // code to execute if condition evaluates to false
    }

- Conditions have a Boolean answer (either true or false)
  - Condition examples:
    - `if (x > 0)`
    - `if (name == 'Bob')`
    - `if (x == y)`
    - `if (x != 5)`
    - `if (x != null)`

## Switch Statements

---

`switch()` is just like if/else but simpler to read and understand

- Format of `switch()` - this is using cases for numbers (can do strings too)

        switch(`variable that evaluates as boolean or takes on other discrete # of values`) {
            case `value1`:
                ... do something ...
                ... do something, etc. ...
                break;
            case `value2`:
                ... do something ...
                ... do something, etc. ...
                break;
            default:
                ... do something ...
                ... do something, etc. ...
                break;
        }

- `value1` and `value2` are values of the variable controlling the switch statement that act as conditions
  - i.e. can be case `(name=='John'):`, or case `(num==4):`, etc.
- A switch trick: switch on the value `true` so the cases can be conditional - that is, based on whether a condition is true (and so matches the switch) or false
  - For example:

        var weight = 135
        switch(true) {
            case (weight == 135):
                alert("Good Weight!")
                break
            default:
                alert("Bad Weight!")
        }

## Try-Catch Handling

---

### Try-Catch logic

- `try` lets you define a block of code to test for errors
- `catch` set up a block of code to execute in case of an error
- `throw` create custom error messages instead of the standard JavaScript errors
- `finally` lets you execute code, after try and catch, regardless of the final result

### Error Name Values

- `name` sets or returns the error name
- `message` sets or returns an error message in string form
- `EvalError` an error has occurred in the `eval()` function
- `RangeError` a number is "out of range"
- `ReferenceError` an illegal reference has occurred
- `SytanxError` a syntax error has occurred
- `TypeError` a type error has occurred
- `URIError` an `encodeURI()` error has occurred
