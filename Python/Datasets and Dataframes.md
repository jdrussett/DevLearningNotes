# Datasets and Dataframes

## Basics

---

To work with data using pandas library, data must be in format of **dataframe**; use `.read_csv()` method in pandas library

- Some useful attributes of dataframes include:
  - `axes` - index and column labels
  - `columns` - column labels
  - `dtypes` - data types in each column
  - `index` - index labels
  - `shape` - ordered pair that gives number of rows and columns
  - `size` - number of values in the dataframe
  - `values` - values in the dataframe
- Some useful methods on dataframes  include:
  - `.describe()` - summary statistics for numerical columns
  - `.head()` - first five rows of the dataframe
  - `.tail()` - last five rows of the dataframe
  - `.min()` - minimum value in a numerical column
  - `.max()` - maximum value in a numerical column
  - `.mean()` - mean of a numerical column
  - `.median()` - median of a numerical column
  - `.std()` - standard deviation of a numerical column
  - `.var()` - variance of a numerical column
  - `.sample()` - random row of a dataframe
  - `.count()` - counts number of rows in a dataframe
  - `.mad()` - mean absolute deviation of a column in a dataframe

Access columns of a data frame with bracket notation; pass a list of columns to access multiple columns at once

- Accessing a column with single brackets returns a series
- Accessing a column with double brackets returns a dataframe; even if only single column is specified
- Stores values of columns and row indices

Can access multiple consecutive rows/columns of data frame with slice notation

Take filtered subset of a dataframe by specifying qualification criteria as part of bracket notation; nested bracket notation

- Example:

        dataframe_subset = dataframe[dataframe[column] == some criteria]

- Could also use `dataframe.column` to set equal to some criteria

`loc[]` function selects subset of dataframe by specifying range of rows using slice notation and list of columns with list notation

`iloc[]` function selects subset of dataframe by specifying range of rows using slice notation and range of columns using slice notation

Dataframe is in **long form** when each column is a variable & each row represents non-repeated data; also referred to as unstacked/record form

Dataframe is in **wide form** when each variable is in a different column; also referred to as stacked

**Pivoting** converts data from long to wide form

`Pandas.pivot()` method will take a subset of a dataframe and create a pivoted data frame based on arguments passed

- First argument is dataframe used
- **index** specifies column values of original dataframe to serve as index labels of pivoted dataframe
- **columns** specifies column values of original dataframe to serve as columns of pivoted dataframe
- **values** specifies column values of original dataframe to serve as values of pivoted dataframe

**Melting** converts data from wide to long form

`Pandas.melt()` method will take a wide form dataframe or subset and convert it into a long form dataframe/subset

- First argument is dataframe used
- `id_vars` argument indicates string/tuple/list to use as identifier variable for melted dataframe
- `var_name` argument indicates column label to use for variable column for melted dataframe
- `value_vars` indicates labels of columns to unpivot for melted dataframe
- `value_name` indicates column label to use for value column
- `.dropna()` method in pandas library will drop any observations with any `NA` values
