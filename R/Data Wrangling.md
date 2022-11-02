# Data Wrangling

## General

---

- `mutate()` can create new variables, either temporarily for plotting or to be added to a data set or subset
  - Example: to create categories from numerical variable, pipe data into `mutate()` function & define new variable as:

        mutate(
            new_var = cut(
                num_var, 
                breaks = c(x1, x2, x3, … , xn), 
                labels = c("label1", "label2", "label3", … , "labeln-1")
            )
        )

    > This will split numerical variable into (n-1) categories specified by n cutoff points; name each new level of categorical accordingly

*Like `ggplot2`, `dplyr` package offers language for data wrangling:*

| **`dplyr` function** | **Description** |
| --- | --- |
| `Select()` | Takes subset of columns/variables |
| `Filter()` | Takes subset of rows/observations |
| `Mutate()` | Adds/modifies existing columns/variables |
| `Arrange()` | Sorts rows/observations |
| `Summarize()` | Aggregates data across rows/observations (groups according to some criteria) |

> - Each function takes data frame as first argument & returns modified version of that data frame
> - Concatenate arguments to filter() function with a '&' operator

- `Mutate()` & `rename()` provide capability to create/redefine/rename variables
  - Declare new variable on a data frame with `mutate()` function with following syntax:

            `data_frame` %>% mutate(`new_column` = ...)

- `Arrange()` sorts a data frame based on column name passed
  - Have to specify data frame & column, may optionally specify sort direction (`asc()` or `desc()`)
  - Can pass multiple columns to sort by (separate columns with commas)
- `Summarize()` almost always used with `group_by()` function
  - Used by itself, `summarize()` collapses data frame into single row
  - Specify parameters/variables you want to see (and how they're calculated, if you provide an alias)
  - All variables in output defined by operations performed on vectors
  - Good for multiple variables

> - `fct_relevel()` is a useful function to reorder the factor levels
> - `case_when()` will execute a find/replace type function over a column/variable (have to specify each individual case)
>   - Example:
>
>           dataset$variable2 <- mutate(
>               case_when(
>                   variable1 > value ~ result1,
>                   variable1 == value ~ result2,
>                   variable1 < value ~ result3
>               )
>           )
>
> - `sample_n()` takes random sample of data set of size you specify with `size = ''` parameter
> - `rep_sample_n()` takes many repeated samples, still of size you specify with `size = ''` parameter, but also with # of repetitions you specify with `reps = ''` parameter
>   - i.e. a `rep_sample_n()` with `reps = 1` is just a `sample_n()`

*Useful dplyr string-related functions:*

- `starts_with()` identifies every string element/variable that starts with character(s) passed
- `ends_with()` identifies every string element/variable that ends with character(s) passed
- `contains()` identifies every string element/variable that contains character(s) passed
- `matches()` identifies every string element/variable that matches character(s) passed
- `num_range()` identifies every string element/variable that starts with character(s) passed and is appended with a digit/digits in the range of integers passed
  - Pass both a string and an array of numbers
- `one_of()` identifies every element that appears in a vector of character elements passed
- `stringr::str_detect()` returns boolean value based on whether a string of characters is found to be contained in another string element/variable passed
- `lubridate::mdy_hms()` extracts date/time as month-day-year, hour-minute-second out of a timestamp
  - Lots of other useful timestamp data extraction functions available in lubridate package

## Data wrangling with dplyr & tidyr: cheat sheet

---

### From dplyr

#### Wrangling conventions

- `tbl_df()` - converts data to `tbl` class; easier to examine than data frames
- `glimpse()` - information-dense summary of `tbl` data or data frame
- `View()` - view data set in a spreadsheet-like display
- `%>%` - pipe operator; passes object on left-hand as argument of function on the right-hand side

> - Regarding order:
>   - `x %>% f(y) == f(x, y)`
>   - `y %>% f(x, ., z) == f(x, y, z)`
>   - So passing a "`.`" as a placeholder with reserve a spot for whatever you're piping in

#### dplyr: Reshaping data

- `data_frame()` - combine vectors into a data frame
- `arrange()` - order rows by values of a column (low to high); pass column inside the `desc()` function to order by high to low
- `rename()` - rename columns of a data frame

#### Subsetting observations

- `filter()` - extract rows that meet logical criteria
- `distinct()` - remove duplicate rows from the selection
- `sample_frac()` - randomly select a fraction of rows
- `sample_n()` - randomly select a positive number of rows
- `slice()` - select rows by position (like Python)
- `top_n()` - select & order the top n entries (by group, if grouped data)

#### Subsetting variables

- `select()` - select columns by name or helper function
- Helper functions available for the `select()` function (pass all as parameter to `select()`):
  - `contains()` - select columns whose names contain a character string
  - `ends_with()` - select columns whose names end with a character string
  - `everything()` - select every column
  - `matches()` - select columns whose names match a regular expression
  - `num_range()` - select columns named as the character string you pass appended by any number in a vector of numbers you pass
    - i.e. `data %>% select(num_range("hello", 1:4))` will select any column named hello1, hello2, hello3, or hello4
  - `one_of()` - select columns whose names are in a group of names (pass a column vector of character strings as a parameter)
  - `starts_with()` - select columns whose names start with a character string
- Can also select columns between two columns, inclusive, based on index, with slice notation ("`:`")
- Can select all columns except for a column or group of columns with "`-`" (use slice notation again for a group)

#### Summarizing data

- `summarise()` - summarize data into single row of values (have to pass aggregating function as a parameter; like `mean`, `sd`, etc.)
- `summarise_each()` - apply summary function to each column (pass `funs()` function as parameter with an aggregating function included to be performed on all columns)
- `count()` - count number of rows with each unique value of a variable
- Aggregating functions that can be used with `summary()`:
  - `first()` - first value of a vector
  - `last()` - last value of a vector
  - `nth()` - nth value of a vector
  - `n()` - number of values in a vector
  - `n_distinct()` - number of distinct values in a vector
  - `IQR()` - interquartile range of a vector
  - `min()` - minimum value of a vector
  - `max()` - maximum value of a vector
  - `mean()` - mean value of a vector
  - `median()` - median value of a vector
  - `var()` - variance of a vector
  - `sd()` - standard deviation of a vector

#### Make new variables

- `mutate()` - compute/append one or more new columns
- `mutate_each()` - apply window function to each column (pass `funs()` as a parameter with a function inside)
- `transmute()` - compute one or more new columns and drop original columns
- `mutate()` uses one or more window functions, which take a vector of values and return another vector of values:
  - `lead()` - copy of values, shifted by 1
  - `lag()` - coppy of values, lagged by 1
  - `dense_rank()` - ranks with no gaps
  - `min_rank()` - ranks; ties get a minimum rank
  - `percent_rank()` - ranks rescaled to [0, 1]
  - `row_number()` - ranks; ties go to the first value
  - `ntile()` - bin vector into n buckets
  - `between()` - boolean returning whether values are between two values passed
  - `cume_dist()` - cumulative distribution
  - `cumall()` - cumulative all
  - `cumany()` - cumulative any
  - `cummean()` - cumulative mean
  - `cumsum()` - cumulative sum
  - `cummin()` - cumulative minimum
  - `cummax()` - cumulative maximum
  - `cumprod()` - cumulative prod
  - `pmax()` - element-wise maximum
  - `pmin()` - element-wise minimum

#### Grouping data

- `group_by()` - group data into rows with the same value of a variable passed
  - Can pass multiple variables; will group by first variable passed, then next one, then next one, etc.
- `ungroup()` - remove grouping information from data frame

#### Combining data sets

Mutating joins:

- Work with data from multiple related tables, linked to each other with keys
  - Match rows that have same value in corresponding column of both tables with `inner_join()`
  - Example:

        data_frame1 %>% inner_join(data_frame2, by = c("common_column" = "common_column"))
  
  - This will result in a set of only rows with matches in both tables
- ``left_join(`data_set1`, `data_set2`, by="`column`")`` - join matching rows from `data_set2` to `data_set1` based on column
  - always returns rows of first table specified, whether there is a match in the second table or not
    - NAs will be inserted into columns/rows with no matched data found
    - Useful in databases with fractured referential integrity
- ``right_join(`data_set1`, `data_set2`, by="`column`")`` - join matching rows from `data_set1` to `data_set2` based on column
- ``inner_join(`data_set1`, `data_set2`, by="`column`")`` - join data from both data sets; retain only matching rows in both sets
- ``full_join(`data_set1`, `data_set2`, by="`column`")`` - join data from both data sets; retain all values and rows

Filtering joins:

- ``semi_join(`data_set1`, `data_set2`, by="`column`")`` - all rows in `data_set1` that have a match in `data_set2` based on column
- ``anti_join(`data_set1`, `data_set2`, by="`column`")`` - all rows in `data_set1` that do not have a match in `data_set2` based on column

Set operations:

- `intersect()` - rows that appear in both data sets passed
- `union()` - rows that appear in either data set passed
- `setdiff()` - rows that appear in first data set passed but not second

Binding:

- `bind_rows()` - append rows of second data set passed to first data set as new rows
- `bind_cols()` - append second data set passed to first data set as new columns (matches rows by position)

### From tidyr

#### tidyr: reshaping data

- `gather()` - gather columns into rows
- `spread()` - spread rows into columns
- `separate()` - separate one column into several
- `unite()` - unite several columns into one

## Text Mining

---

- `tidytext::unnest_tokens()` splits columns into tokens using tokenizers package, splitting table into one-token-per-row
- `tidytext` library also has text sentiment analysis capabilities
  - `get_sentiments()` retrieves lexicon sentiment values for different words
    - Can pass ``lexicon = `parameter` ``, types include "`nrc`", "`bing`", "`afinn`"

> Pretty intense stuff on this in the 365NotesTextMining file(s) in file:///C:/Users/Jake%20Russett/OneDrive/Documents/Creighton%20Archive/MTH%20365/365NotesTextMining.html
