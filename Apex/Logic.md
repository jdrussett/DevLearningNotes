# Logic

## Try-Catch

---

Use try-catch handling to catch and handle possible error conditions

*Format:*

    try {
        … code to execute that you want to succeed …
    } catch ([error_type] [error_variable]) {
       … code to execute if an error is caught …
    }

## Loop Statements

---

### For Loops

*For loop traditional format:*

    for (Integer [count_var] = 0; [count_var] < n; [count_var] ++) {
       … code to execute …
    }

*For loop iteration container format:*

    for ([data_type] [looping_var] : [iteration_collection]) {
       … code to execute …
    }

> Data type of the looping variable must be the same data type as the data stored in the iteration collection

### While Loops

> Checks condition before loop starts

*Format:*

    while ([condition]) {
       … code to execute …
    }

### Do-While Loops

> Checks condition after loop starts (always runs at least once)

*Format:*

    Do {
       … code to execute …
    } while ([condition])

## If-Else Statements

*Format:*

    if ([condition1]) {
       … code to execute …
    } else if ([condition2]) {
       … code to execute …
    }

## Switch Statements

> Provide an alternative to if-else statements, if condition is fairly simple

*Format:*

    switch on [expression_or_variable]{
       when [value1] {
          … code to execute …
       }
       when [value2] {
          … code to execute …
       }
       when [value3] {
          … code to execute …
       }
    }

> Can use multiple values for a particular 'when' node by separating them with commas
