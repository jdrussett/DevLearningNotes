# Data Types and Definition

## General

---

- `<-` assignment operator is used to define any basic object in R

Functions that help with learning about an object:

| **Function** | **Description** |
| --- | --- |
| `attributes()` | Displays attributes associated with an object |
| `typeof()` | Provides information about underlying data structure of objects |
| `str()` | Displays structure of an object |
| `mode()` | Displays storage mode of an object |
| `glimpse()` | Provides useful summary of each variable for data frames |

- R supports object-oriented programming
  - `help(UseMethod)` provides detail
- Objects in R have associated *class* attribute
  - `class()` returns class to which an object belongs
  - Class membership of an object determines default behavior for certain operations on the object
  - Many functions called *generics* have special capabilities when applied to objects of a particular class
    - Example: calling `summary()` on object of type `lm` (linear model) implicitly calls function `summary.lm()`
  - Specific implementations of generic functions are called methods
  - `Methods()` function displays all classes supported by generic function
- Arguments of functions in R always separated by commas
- `Print()` & `summary()` functions of an object will return the object or the summary of it, respectively

> **Pipe-forwarding** with pipe operator `%>%` is better than nesting functions
>
> - Example: `` `data_frame` %>% filter(`condition`)`` is easier to understand than ``filter(`data_frame`, `condition`)`` if more & more statements are added

- `nchar()` finds length of a string
- `factor()` shows the factors underlying a categorical variable
- `floor()` rounds down to nearest integer
- `ceiling()` rounds up to nearest integer
- `levels()` provides all the distinct factor levels of a categorical variable
- `reorder()` treats first parameter as categorical variable and reorders its factors according to second parameter variable, which is treated as numeric

## Object Definition

---

### Vectors/Lists

`c()` function will create a vector that concatenates scalars or other objects in R

- Can also define vector with specific metadata:

        vector_name <- vector("data_type", length_limit)

- `length()` accesses the length of a vector
- A *factor* is a special type of vector for categorical data that has different levels that can be accessed with `levels()` function
  - `relevel()` allows changing reference level of a factor/reordering the levels
  - Factors are stored internally as integers that correspond to the id's of the factor levels
  - An option encouraged for data wrangling is `stringsAsFactors = FALSE`
- Accessing vector elements:
  - `` `vector_name`[`i`]`` will return the `i`th element of `vector_name`
    - Indexing begins at 1
  - `` `vector_name`[c(`i`, `j`)]`` will return all elements from the `i`th to the `j`th element (inclusive) of `vector_name`
  - `` `vector_name`[-`i`]`` will return all elements of `vector_name` before the `i`th element
  - `help(Extract)` will provide help on object extraction mechanisms
- Executing the command `` `vector_name` > `α` `` will return a Boolean value for each element of `vector_name` indicating whether the element is greater than the scalar `α`
- Members of a list in R can be named/referenced using numeric indices using the `[[]]` operator
  - Lists in R are general objects that can contain other objects of arbitrary types
  - `unlist()` makes a vector out of the elements of a list that you pass
- `%in%` operator checks to see whether value is contained in specified vector
- `sort()` will sort a vector but not a data frame
- `n_distinct()` counts number of distinct rows/values in a column specified
- `seq()` function creates a general sequence; pass parameters `from =` , `to =` , and `by =` to define start and end points of the sequence and step size
- `list()` defines a list; lists are compatible with $ operator to access their elements
- `length()` finds length of a vector/column variable or other container object
- `range()` returns the highest/lowest elements of a vector passed
  - Can't process `NA`s or infinities, have to pass `na.rm = TRUE` and `finite = TRUE` if have either of those things in the vector
- ``rep(`x`, `n`)`` function will create `n` repetitions of the value `x` passed in the form of a vector/list

### Matrices/Data Frames

`matrix()` defines a matrix

- passing a vector and two numeric parameters to split matrix into rows and columns
  - Example: if vector `x = c(5, 7, 9, 13, -4, 8)`, then `matrix(x, nrow = 2, ncol = 3)` will output: (rows comes before columns by default)

                [,1]    [,2]    [,3]
            [1,]  5       9      -4
            [2,]  7      13       8
  
  - Elements of matrices can be called via same call method as elements of vectors, but now have to specify both parameters of column & row (or only specify one, will return a whole column or a whole row)
- Data sets are often stored in **data frames** in R, which is basically a special list that is a more general matrix
- Can also create a simple data frame with `data.frame()` function
- `$` operator used to access an object/column within a data frame
  - `With()` function will also work
- *Rename column of a dataframe*:

        names(`data_frame`)[names(`data_frame`) == "`old_column_name`"] <- "`new_column_name`"

- `Nrow()` returns the number of rows in a matrix/data frame
- `Ncol()` returns the number of columns in a matrix/data frame
- `Dim()` returns dimensions of a matrix/data frame
- Length of a matrix/data frame is equal to number of columns times number of rows, or the product of the elements of its dimension
- Data frames always have names of variables, accessed with `names()`, and sometimes have row names, accessed with `rownames()`
- Data frames are lists of vectors of same length
- Data sets typically have class *data.frame* but are of type *list*
- `Names()` provides names of all variables of data set
  - Pass data set as argument
- `rename()` lets you rename column of a data frame
  - Example: `` `dataset` %>% rename(`new_column_name` = `old_column_name`)``
- `n()` or `nrow()` counts number of rows in a data frame
- **data.frame** is base object in R (data table); columns within data frames are vectors
- `names()` returns column names of a data set passed
- Can use bracket notation to return specific rows, columns, or data points of a data set
  - `` `data_set`[1,4]`` - get data point at first row, fourth column
  - `` `data_set`[1,]`` - get first row of data
  - `` `data_set`[,4]`` - get fourth column of data
  - *Slice notation* also supported
- `$` operator gets a column of a dataset
- `glimpse()` and `head()` both give insight into data set
  - `glimpse()` gives column definitions and some data
  - `head()` gives data
    - `head()` gives the observations in their default/descending order, `tail()` is the opposite of `head()`

        > gets observations ascending from the bottom first

- ``attrbiutes(`data_frame`)`` yields names of columns & rows, and class of objects we could interact with the data frame as
- `pull()` works like double bracket notation `[[]]` for a data frame, but for a **tibble** (pulls out a single variable at a time)
- `complete.cases()` will only select observations in a data set passed with no missing values for any variables
- `expand.grid()` takes two vectors as parameters and creates table of every possible pairing between both vectors' elements
- `colnames()` gets the column names of a table/data frame object
- `rbind()` adds rows to a matrix, `cbind()` adds columns to a matrix
- ``summary(`data_set`)`` gives summary statistics on a data set
  - Can add other parameter functions to summary, like `group_by()` or `filter()`
- `tibble()` creates a tibble
- `add_column()` adds a vector as a column to a data frame

## Data Type Prefixes

---

`is.` data type prefix can be appended to the front of a data type function to determine whether a passed object is of that data type

- Will return a boolean value
- Examples: `is.vector()`, `is.matrix()`, `is.data.frame()`
- Special case: `is.na()` checks to see if passed argument has value of `NA`
- `is.data_type()` returns a boolean value indicating whether the object passed is of the data type you specified

`as.` data type prefix can be appended to the front of a data type function to change an object into that data type, if it is compatible

- Example: `as.data.frame()` creates data frame out of matrix or other compatible substitute, `as.matrix()` creates matrix out of data frame or other compatible substitute, etc.
- Other examples: `as.factor()`, `as.numeric()`, `as.data.frame()`, etc.

## Reading in Data

---

- ``readr::read_csv("`file_path\file_name.extension`")`` reads in a data set stored at whatever file path/file name you specify as a data frame object
- ``read.csv(`file_path`)`` reads a CSV file stored in a local file directory on your machine
  - Can begin path at local/working directory in Rstudio if prefaced with "`~/`"
- Import data with any of the following functions: `read.csv()`, `read.text()`, `read.table()`
  - `Use read.csv()` for a data frame object type, use `read_csv()` for a tibble object type
- ``readxl::read_excel(`file_path_to_excel_doc`)`` will read excel table & automatically populate table with data in R

## Advanced

---

- `paste()` combines results from multiple variables into one new variable, passing each variable/variation of a variable as a parameter & passing a delimiting character as a parameter with ``sep = "`character`"``
  - **Very useful!!** See file:///C:/Users/Jake%20Russett/OneDrive/Documents/Creighton%20Archive/MTH%20366/MTH366_HW8.html for reference of use
- `I()` identity function allows you to declare a new variable based on the function of another variable

## Tidy and Untidy Data

---

*Tidy vs. untidy data:*

Example: **untidy**

| Country | Year 1 rate | Year 2 rate | Year 3 rate | Year 4 rate |
| --- | --- | --- | --- | --- |
| A | 0.1 | 0.1 | 0.2 | 0.3 |
| B | 0.4 | 0.1 | 0.1 | 0.1 |
| C | 0.5 | 0.6 | 0.1 | 0.2 |

Example: **tidy**

| Country | Year | Rate |
| --- | --- | --- |
| A | 1 | 0.1 |
| A | 2 | 0.1 |
| A | 3 | 0.2 |
| A | 4 | 0.3 |
| B | 1 | 0.4 |
| B | 2 | 0.1 |
| B | 3 | 0.1 |
| B | 4 | 0.1 |
| C | 1 | 0.5 |
| C | 2 | 0.6 |
| C | 3 | 0.1 |
| C | 4 | 0.2 |
