# Logic

## Boolean Operators

---

| **Boolean Operator** | **Description** |
| --- | --- |
| `` `expression_1` and `expression_2` `` | True when both `expression_1` and `expression_2` are true |
| `` `expression_1` or `expression_2` `` | True when either `expression_1` or `expression_2` are true |
| ``not `expression_1` `` | True when `expression_1` is false |

## Loops

---

**While loops** can be written with a simple line:

    While `condition to check if true`:

> need a colon to punctuate the line & begin the loop

- While loops supported for statements that repeat until condition is no longer true
  - Example:

            while `variable` `relational operator` `conditional statement`:

**For loops** supported for specified number of iterations of a statement to execute

- Can run a for loop over elements of a container in two ways:
  1. Iterate over indices
     - Example:

            list = [...];
            for x in range(len(list)):
                ...

  2. Iterate over values
     - Example:

            list = [...];
            for x in list:
                ...

- `Enumerate()` function yields new tuple for each iteration of a loop containing both the index and value of a list iterating over
- If looping over a string, have to use ``range(len([`string`]))`` to cause the loop to iterate over each character in the string

## If-Else Statements

---

If-else statements written with syntax:

    If `general statement of logic`:
        `code to execute`
    Elif `general statement of logic`:
        `code to execute`
    Else `general statement of logic`:
        `code to execute`

> For `If` statement line, no brackets/parentheses required; have to punctuate end of each line with a colon to indicate logical operator
> For code to execute, no ending punctuation required to end line
> Can have multiple `Elif` clauses in one `if-else` statement

- Key for if-else statements is *indentation*; indentation puts line of code within parent logical statement
- **Conditional expressions** are like inverted if-else statements with only two branches printed next to each other on same line
  - Format is: ``expression if true` if `condition checked` else `expression if false` ``
  - Good practice is to restrict usage to assignment statements only
    - Example:

            y = 5 if (x <= `test_value`) else 0

    > Only condition can have parentheses around it, only `expression if true` can contain `"object of interest = "`
