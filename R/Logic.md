# Logic

## If/Else Statements

---

- R supports typical `ifelse()` function syntax

        ifelse(`condition`, `value_if_true`, `value_if_false`)

- Can also use regular iterative logic

        if(condition_to_meet) {
            code_to_iterate_if_true
        } else {
            code_to_iterate_if_false
        }

## Loops

---

- For loops defined as:

        for ( `iterative_logic` ) { 
            `code_to_iterate`
        }

  - Use `in` to loop a variable through a container
- Use `:` to set loop beginning & end (i.e. `for i in 1:nrow(data_set)`, or `for i in 1:length(vector)`)
