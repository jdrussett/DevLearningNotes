# Error Handling

## General

---

- R will denote missing values in data frame with '`NA`'
- R uses `NA` to represent missing values in data structures
- `NaN` and `Inf` are both outputs to denote "not a number" and "infinity", respectively
- `na.rm = TRUE` as an argument will dynamically remove missing values from whatever container you're working in
- `is.na()` checks to see if a data item is `NA`
  - Returns boolean value; i.e. if `x <- NA`, then `is.na(x) == TRUE`
- `na.omit()` when applied to a data frame will only keep observations with no values of '`NA`' in any of the columns
