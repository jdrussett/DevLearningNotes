# Visualization

## Basics

---

`matplotlib` package can be used to create plots in Python; replicates plotting capability of MATLAB

> Also requires `Numpy` package

`matplotlib.show()` function displays a created/defined graph

`matplotlib.plot()` function plots data on the graph

- Accepts various arguments; lists of x-coordinates & y-coordinates from the data, for example
- If only one list passed, `plot()` uses 0 & all positive integers as values for x
- Calling `plot()` multiple times will simply draw multiple lines on the same created graph
- Can pass optional argument format string to specify color and style of plotted line
  - Example: ``plot(`x`, `y`, 'r--')`` will plot a red dashed line of x-values and y-values

`matplotlib.savefig()` function saves graph to a file

Characters to specify line/color style:

| **Character** | **Color or style** |
| --- | --- |
| `b`| Blue |
| `g`| Green |
| `r`| Red |
| `w`| White |
| `k`| Black |
| `y`| Yellow |
| `m`| Magenta |
| `c`| Cyan |
| `-` | Solid line |
| `--`| Dashed line |
| `-.`| Dashed-dot line |
| `:` | Dotted line |

Characters to specify marker (point) type:

| **Character** | **Marker type** |
| --- | --- |
| `.` | Point |
| `,` | Pixel |
| `o` | Circle |
| `+` | Plus |
| `X` | X marker |
| `V` | Triangle-down |
| `^` | Triangle-up |
| `<` | Triangle-left |
| `>` | Triangle-right |
| `*` | Star |
| `p` | Pentagon |
| `1` | Tri-down |
| `2` | Tri-up |
| `3` | Tri-left |
| `4` | Tri-right |
| `h` | Hexagon1 |
| `H` | Hexagon2 |
| `D` | Diamond |
| `d` | Thin diamond |
| `|` | Vertical line |
| `_` | Horizontal line |
| `s` | Square |

Format strings are all really just shortcuts for setting **line properties**: attributes of line object created by `matplotlib` when `plot()` is called

- Determine how line will appear when it is produced by `show()`

Line properties include:

| **Property** | **Acceptable Input** | **Description** |
| --- | --- | --- |
| `alpha` | Float data type | Enables transparency |
| `antialiased` | Boolean data type | Enabled anti-aliasing of the line |
| `color` | *(a matplotlib color)* | Color of the markers/line |
| `solid_capstyle` | 'butt', 'round', or 'projecting' | How the cap of a line appears |
| `solid_joinstyle` | 'miter', 'round', 'bevel' | How the join of a line appears |
| `data` | *(data supplied to graph)* | List of lists of x-values and y-values |
| `label` | String data type | Label to use for the line |
| `linestyle` | *(see above)* | Style of the line |
| `linewidth` | Float data type | Width of the line when it's drawn with show() |
| `marker` | *(see above)* | Style of marker to use |
| `markersize` | Integer data type | Size of each marker |
| `visible` | Boolean data type | Show/hide the line |

`legend()` function will display legend of the lines in the plot area created by `show()` function

- Have to specify particular region of the plot area to place the legend, like "upper right"

`xlabel()` and `ylabel()` functions can be used to give the axes of a plot titles

`title()` specifies the title of a plot

- `fontsize` argument specifies size of font to be used (probably for more than just title function)

`axvline()` and `axhline()` are functions to add lines at specific x- or y-values on the graph area

`text()` function will add text in the form of a label to the plot area at x- and y-value that you specify

- Sequence of arguments is x-value, y-value, string

`annotate()` function creates annotation that links text label with specific data point

- Specify coordinates of text label and data point and arrow will automatically be drawn from text pointing to data point
- First argument is text label to be displayed, second argument designates data point arrow will point to, ``xy=(`x-value`, `y-value`)``, third argument designates where text label will appear & arrow will be drawn from, ``xytext=(`x-value`, `y-value`)``
- Arrow's appearance can be customized by defining dictionary of arrow properties

`Numpy` package provides tools for scientific/mathematical computation in Python

- Uses **array** data type that is similar to a list (ordered set of elements of same type); can be created using array() function from numpy package
- Multidimensional arrays created by specifying list with tuple each dimension's elements

Sometimes arrays have to be created before element values are known --> numpy provides functions to create pre-sized empty arrays

- `zeros()` creates array with 0's for every element; takes argument of tuple specifying number of rows & columns, respectively
- `ones()` creates array with 1's for every element; takes argument of tuple specifying number of rows & columns, respectively

`linspace()` creates sequence be segmenting given range with specified number of points

- Arguments are start value, end value, number of points

`figure()` function can be used to create multiple **figures**: corresponds to window frame to be opened by `matplotlib`, and each figure can contain plot that uses different axes

- Ideal when trying to plot 2+ graphs that cause the plot to become cluttered/unhelpful to look at all on one window
- Simply call `figure()` function in the script & pass the name of the figure to activate
  - All changes/edits made to plot properties will correspond to that figure until new figure is specified
- First figure will always be produced by matplotlib automatically in the background

`axis()` function used to set range of x- & y-axes; argument is single list of x and y minimum & maximum values

- Format:

        axis(`x_min`, `x_max`, `y_min`, `y_max`)

`subplot()` function allows multiple plots to be created in a single figure using same axes but with each subplot having its own copy of the set of axes

- Preferable to using multiple figures when related data is being plotted
- First/second arguments specify number of rows/columns to use, respectively; third argument specifies current active subplot

`twinx()` method creates a second axis on the plot

- Adding second y-axis sometimes allows for combining different types of data to be graphed on same plot
- Used in conjunction with `add_subplot()` method

Creating basic plot:

    dataframe_variable = pandas.read_csv('[dataframe csv file]')
    matplotlib.pyplot.title('[give the plot a title here]')
    matplotlib.pyplot.xlabel('[give the plot an x-axis label here]')
    matplotlib.pyplot.ylabel('[give the plot a y-axis label here]')
    matplotlib.pyplot.plot(dataframe_variable["xvariable"], dataframe_variable["yvariable"])
    Matplotlib.pyplot.savefig("image_name.png")

`Seaborn.countplot()` function plots categorical data with respect to different categories

- Pass arguments `x` or `y` and set equal to categorical variable
- Pass argument `data` to specify source dataframe

Setting **hue** equal to a categorical variable will create count/frequency of each factor level of variable specified

`matplotlib.subplots()` function used to create stacked bar chart

`matplotlib.pie()` function used to make pie charts

- `sizes` argument is list parameter that consists of frequencies of each group/category being graphed
- `labels` argument is list parameter that consists of names of each group/category being graphed
- `autopct` is optional argument that number of decimal places of percentage labels
- `explode` is optional argument to explode out one or more categories in a pie chart

`seaborn.regplot()` function will graph a scatter plot

- Arguments `x` and `y` take in vectors of explanatory/response variables
- Optional argument `ci = None` can be specified to disable confidence interval output (set to 95% by default)

`seaborn.stripplot()` creates a strip plot (plots points to represent count values according to category; like a box plot but with points)

- One variable is numerical, one is categorical
- Optional argument `jitter = True` will add jittering to plot to see quantity of points at each level

`seaborn.swarmplot()` function creates swarm plot; like a jitter plot, but points are stacked in orderly way to convey frequency at a particular level

- Again optional argument **hue** can be set to differentiate color based on some other categorical variable

`seaborn.boxplot()` function creates a boxplot

`Matplotlib.pyplot.hist()` will create a histogram

- `bins` argument can be passed to specify number of bins

`seaborn.violinplot()` function creates violin plot

- Specify either x or y axis to plot numerical variable
- Create stacked barplots according to several factors of categorical variable by specifying categorical on other axis
- Create side-by-side violin plots by specifying hue argument to another categorical
- Specify `split = True` if you want violin plots to be conjoined along the same spine

Creating a 3D plot:

    from mpl_toolkits.mplot3d import Axes3D
    dataframe_variable = pandas.read_csv('[dataframe csv file]')
    figure_variable = matplotlib.pyplot.figure()
    axes_variable = figure_variable.add_subplot(111, projection = '3d')
    axes_variable.scatter(dataframe_variable["yvariable"], dataframe_variable["x1variable"], dataframe_variable["x2variable"], c = 'b', marker = 'o')
    axes_variable.set_xlabel('x1variable axis name')
    axes_variable.set_ylabel('x2variable axis name')
    axes_variable.set_zlabel('yvariable axis name')
