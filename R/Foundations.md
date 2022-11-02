# Foundations

## Packages

---

To use packages, first have to *install* and then *instantiate* in a markdown document or script

- Useful, commonly available libraries:

| **Library name** | **Notes** |
| --- | --- |
| `dplyr` | For data wrangling; `select()`, `arrange()`, `filter()`, `mutate()`, `summarize()`; required for deep learning |
| `tidyverse` | For making data tidy, contains `ggplot2`, Hadley Wickham's gift to the world |
| `mosaic` | Contains a bunch of other packages |
| `mdsr` |  |
| `ggplot2` | For tidy plotting conventions and protocols |
| `openintro` |  |
| `skimr` |  |
| `airlines` (see also: `nycflights13`) | Contains good sample data |
| `Lahman` |  |
| `babynames` | Contains good sample data |
| `fec` |  |
| `macleish` |  |
| `IMDbPY` |  |
| `twitteR` |  |
| `RColorBrewer` | For coloring graphs/making things look pretty |
| `rvest` |  |
| `beepr` | Full of fun sounds to throw in markdowns/scripts |
| `MASS` |  |
| `keras` | Required for deep learning |
| `tfruns` | Required for deep learning |
| `tfestimators` | Required for deep learning |
| `TensorFlow` | Required for deep learning |
| `ISLR` | Data sets & statistical tools |
| `glm2` | Advanced generalized model building capabilities |
| `faraway` | Some data sets |
| `lme4` | Random effects models library |
| `glmnet` |  |
| `gapminder` |  |
| `dslabs` |  |
| `rpart` | Needed for decision tree construction |
| `rattle` | Needed for plotting features for decision trees |
| `rpart.plot` | Needed for plotting features for decision trees |
| `randomForest` | Needed for random forest modeling |
| `nnet` | Needed to fit single-hidden-layer neural network; use caret or keras for more layers |
| `tidytext` | Needed for text mining |
| `textdata` | Needed for text mining |
| `rvest` | Needed for web scraping |
| `robotstxt` | Needed for web scraping |
| `stringr` | Needed for wrangling data out of strings |
| `lubridate` | Contains useful functions for extracting/transforming date/time data |
| `recipes` | Needed for using recipes with model training |
| `installr` | For updating R from the terminal |

- ``install.packages("`package name`")`` installs a package into RStudio environment; one-&-done for all packages
- `library()` instantiates package into working markdown/script
  - Must be done every time new RStudio session is spun up
- `::` operator accesses functions within packages
  - Can use this shortcut to access function in package without having to instantiate the entire thing
  - Looks like `` `package_name`::`function_name` ``
- `update.packages()` command should be run occasionally to make sure all packages are up to date
- ``library(help="`package_name`")`` will display help information about an installed package
- Run `browseVignettes(package = c("dplyr", "tidyr"))` to learn more about `dplyr` and `tidyr` packages; pretty cool
  - Could theoretically pass other package names...?

## Workspace/Session

---

- `installr::updateR()` updates R from the terminal
- `exists()` - returns whether an object by the name you pass already exists in the current workspace
- `rm()` function will remove an object from the current workspace
  - Remove all objects in workspace with `rm(list=ls())`
- `sessionInfo()` provides version information about R & details of currently loaded packages
- `detach()` detaches a package from a particular workspace
  - Example: ``detach(package:`package name)` ``
- `Objects()` will provide names of all objects within current R session
- `set.seed()` prevents R from re-generating new random sample or other random procedures every time the document is running; bookmarks the randomization start point so each randomized process runs the same way every time
- In an R chunk in a markdown document, in the definition line, setting parameter `eval = -number` or `eval = -c(number, number, ...)` will prevent R script from evaluating specified lines in markdown
  - Also works with other chunk definition functions, like `echo =`, etc.
  - Also try: `results = "hide"`
  - Setting `cache = TRUE` in a chunk will save the result of the code that runs in that chunk from the time it last ran, provided it hasn't changed since then; saves a lot of time when some chunks take a long time to run
  - `fig.width`, `fig.height` are other parameters that can be set in chunk definition
- Neat trick to time how long chunks take to run in a markdown is to declare a variable at the top of the chunk as `start_time <- Sys.time()` and then subtract that variable from `Sys.time()` at the bottom of the chunk; will return overall elapsed time chunk took to run
- To add beeps to R chunks can use `beepr` library and use `beep()` function; something like 13 different beep tone options
- My preferred markdown document output settings:

        output:
            html_document:
                highlight: espresso
                theme: cerulean
                fig_width: 9
                fig_height: 6
            pdf_document:
                highlight: espresso
                fig_width: 9
                fig_height: 6

- Insert LaTeX into a markdown by surrounding the code with `$` delimiters for in-place TeXing, or with `$$` for centered and indented TeXing
- Comment in script/markdown with `#`
- Create indented alternate-text environments in script/markdown with `>`
- Create italicized text in script/markdown with `*` or `_` delimiters
- Create bolded text in script/markdown with `__` delimiters
- `download.file()` downloads a file from the internet
- `View()` will open up data frame or data set document into new window in Rstudio
- *Theme and highlight options for Rmarkdown documents:*
  - Themes:
    - cerulean
    - cosmo
    - flatly
    - journal
    - lumen
    - paper
    - readable
    - sandstone
    - simplex
    - spacelab
    - united
    - yeti
    - hrbrthemes::ipsum
    - prettydoc::architect
    - prettydoc::cayman
    - prettydoc::hpstr
    - prettydoc::leonids
    - prettydoc::tactile
    - rmdformats::html_clean
    - rmdformats::html_docco
    - rmdformats::material
    - rmdformats::readthedown
    - tint::tintHtml
    - tufte::tufte_html
  - Highlights:
    - tango
    - pygments
    - kate
    - monochrome
    - espresso
    - zenburn
    - haddock
    - breezedark

## Other Help

---

- `?` operator used to see help documentation regarding a function, data set, object, etc.
  - `help()` function will also work
    - Do not include "`()`" on the end of a function name if passing it into `help()`
      - For help on reserved words such as "`if`", "`else`", "`repeat`", etc., put word in quotes when passed to `help()`
- `RSiteSearch()` searches for key words/phrases that you pass in different search destinations for R
- `example()` provides a useful example of the function you pass it in use
- `help.start()` and `help.search()` provide a set of online manuals and can be used to look up entries by description, respectively
- `apropos()` returns the functions in the search list that match a given pattern
  - Facilitates searching for a function based on what it does, as opposed to its name
- `options()` can be used to change various default behaviors of other things in R
  - See `help(options)` for more help on this

## Swirl

---

**Swirl** system is a collection of interactive courses to teach R programming and data science right within the R console

- First have to install the `swirl` package & use the `install_from_swirl()` function to download courses
- Names of available courses are:
  - "R Programming"
  - "R Programming Alt"
  - "Data Analysis"
  - "Mathematical Biostatistics Boot Camp"
  - "Open Intro"
  - "Regression Models"
  - "Getting and Cleaning Data"

## Operators

---

### Arithmetic Operators

| **Operator** | **Description** |
| --- | --- |
| `+` | Addition |
| `-` | Subtraction |
| `/` | Division |
| `*` | Multiplication |
| `^` | Exponentiation |
| `%%` | Modulus division |
| `%/%` | Integer division/floored division |

- See `help(syntax)` for more information

### Boolean Operators

| **Operator** | **Description** |
| --- | --- |
| `|` | Or; operates on each element of a vector |
| `||` | Or; stops evaluation the first time the result of a vector element evaluates to `TRUE` |
| `&` | And |
| `!` | Not |
| `xor()` | And/Or |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `==` | Equal to |

### Other Operators

| **Operator** | **Description** |
| --- | --- |
| `<-` | Assignment operator; reserves a name for a variable defined to the right; defines any basic object in R |
| `[[]]` | Member access operator; used to get elements/members of a list, vector, data frame, tibble, etc. |
| `::` | Function access operator; gets functions from within packages; eliminates need to instantiate package to utilize function |
| `?` | Help operator |
| `$` | Column access operator; used with data frames, tibbles, etc. |
| `%>%` | Pipe operator; passes object on the left into object on the right |
| `%in%` | Inclusion operator; used to check which/if elements are in a container; helpful for filtering mechanisms |
| `:` | "plus 1" operator; defines a "+ 1" list |
| `%+%` | Updates a plot bound to a data frame |
| `|` | Pivoting operator; pivots an operation to each level of a factor; i.e. gets factor-level means, gets factor-level ... other stuff; similar to grouping by |

## Basic Math Stuff

---

- `sqrt()` calculates square root
- `log()` performs the natural log function, ln
- `dist()` calculates distance between two points in Euclidean space
- `round(x, n)` rounds `x` to the `n`th decimal place
- `exp()` is the exponentiation function, raises e to the power passed
- `sum()` calculates the sum of elements passed
- `abs()` takes absolute value
- `pi` is a reserved word for the mathematical constant, Pi
- `MASS::fractions()` returns result in fraction form, if rational
- `sin()`, `cos()`, `tan()` are trigonometric functions, `asin()`, `acos()`, `atan()` are inverse trigonometric functions, `sinpi()`, `cospi()`, `tanpi()` are the trig functions but automatically multiply the input you pass by pi (sort of neat)
