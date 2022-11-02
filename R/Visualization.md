# Visualization

## General

---

- Visualizing missing data:
  - Base R approach:

        data %>% is.na() %>% 
            reshape2::melt() %>% 
            ggplot(aes(x = var1, y = var2, fill = value)) + geom_tile() + labs(x = 'observation', y = 'variable')

  - visdat library approach:

            visdat::vis_miss(data, cluster = TRUE) + coord_flip()

- `plot()` creates a generic plot in base R
  - Parameters include `x`, `y`, `type` (changes plot visual element)
- Code to *evaluate LINE assumptions of a linear model is:*

        par(mfrow = c(2,2))
        plot(lm(model definition))

- `grid.arrange()` will put all plot objects passed to it in one plot window, organized by default arrangement or as you specify with `ncol =` and `nrow =`
- `factoextra::fviz_eig()` creates a scree plot for principal components analysis
- `factoextra::fviz_pca_var()` creates visualization plane for variable contribution to principal components structure
  - Pass `col.var = "contrib"`
- `rattle::fancyRpartPlot()` creates visualization for decision tree model
- `factoextra::fviz_nbclust()` plots optimal number of clusters for a clustering model
  - you deduce optimal, shows you total within sum of squares deviation as k increases
  - Parameters are `data =`, `FUN =`, `method =`, `k.max =`
- `rect.hclust()` draws rectangles around the branches of a dendrogram highlighting the corresponding clusters
  - Pass it an `hclust()` argument as well as `k =` and `border =`

### ggplot2

- `ggplot2::ggplot()` creates a plot in ggplot2; any arguments are applied across subsequent plotting directives; graphics built incrementally by adding elements with `+` or `%>%` operator; in general, if relating a plot element to a variable, must be done within an `aes()` command
  - `geom_point()` plots a point in a two-dimensional plot; added arguments specify how & where points are drawn
    - Aesthetics can be introduced (per the `aes()` command mentioned earlier); used to map variables to the x or y axis
    - `cex =` parameter determines size of plotted points (integers greater than 0)
    - `pch =` parameter determines shape of plotted points (integers greater than 0)
  - `coord_trans()` plotting directive lets you modify one or both plot axes away from just a linear scale
    - E.g. `coord_trans(y = "log10")` will plot log of y variable on vertical axis
  - Scale of a variable/axis can also be manipulated in ggplot2 using any of multiple scale functions
    - `scale_y_continuous()`, `scale_x_continuous()`, `scale_y_discrete()`, `scale_x_discrete()`, `scale_color()`, etc.
      - Pass `trans` parameter to transform the scale (i.e. `trans = "log10"`)
    - E.g. same transformation of y axis as with `coord_trans()` could also be achieved with `scale_y_continuous(trans="log10")`
  - Guides & legends provide context on graph modifications; automatically produced for included plotting directives
    - Argument/directive is `guides(aesthetic = guide_legend('variable'))`
  - **Facets** are multiple side-by-side graphs used to display levels of a categorical variable, provide alternative to cluttering up one graph with lots of graph elements
    - `facet_wrap(~column_name)` creates facet (new graph) for each level of single categorical variable (pass variable as parameter)
      - `scales = "free"` parameter can be added to `facet_wrap()` to allow individual plot axes to vary
    - `facet_grid()` creates facet for each combination of 2 categorical variables (pass variables as parameters)
  - Data from multiple tables can be plotted on the same graph by adding more plotting directives
  - `geom_histogram()` or `geom_density()` plot histogram to help understand single variable/s distribution
    - `binwidth =` argument used to specify width of histogram bins
    - `adjust =` argument used to modify bandwidth used by kernel smoother in density plot
  - `geom_bar()` makes bar graph for categorical variables
    - Passing `stat = identity` argument forces ggplot to use y aesthetic, mapped to whatever you specify
  - `geom_col()` lets you create a bar/column graph while specifying two axes/parameters; represents points as column heights (doesn't require frequency like `geom_bar()`)
  - `coord_flip()` inverts axes of a graph you append it to
  - Can add `xlab()` and `ylab()` as their own plot directives
- To update plot bound to a data frame, use `%+%` operator
  - Example:

        plot_name <- plot_name %+% updated_data_frame

- Can take a subset/sample of a data frame for ggplot using argument `data = sample_n(data_frame, size = n)` where `n` is size of observations you want to take
- *Summary of ggplot graph types:*

| **Response (Y)** | **Explanatory (X)** | **Plot type** | **ggplot command** |
| --- | --- | --- | --- |
| | Numeric | Histogram/density | `geom_histogram()`, `geom_density()`, `geom_violin()` |
| | Categorical | Stacked bar | `geom_bar()` |
| Numeric | Numeric | Scatter | `geom_point()` |
| Numeric | Categorical | Box | `geom_boxplot()` |
| Categorical | Categorical | Mosaic | `graphics::mosaicplot()` |

- `geom_linerange()` adds line intervals to graph; parameters to pass are `ymax` & `ymin`
- `ggplot()` can have data set piped into it, or specify data set with `data =` parameter
  - `aes()` indicates aesthetic elements to a plot
  - `geom_point()`/`geom_bar()` are different types of plot operations
  - Parameter `bins =` sets number of groups included in a histogram; `binwidth =` sets horizontal length of bins
- `geom_histogram()` will produce histogram when concatenated with a `ggplot()`
- `geom_smooth()` adds fancy shaded trend region around trend line
  - Usually use `method = 'lm'` as a parameter; other methods are available
  - Can use `method = 'glm'`, `method.args=list(family = "binomial")`, `se=TRUE` for non-linear smoothed region
- Parameter `alpha =` with any geom function sets transparency level for plotting visual

## Data visualization with ggplot2: cheat sheet

---

### Basics

- **Ggplot2** is based on grammar of graphics: building every graph from same core components: data set, coordinate system, geoms (visual marks representing data points)
- Basic outline of any plot in ggplot2 will be as follows:

      ggplot(data = data) + geom_function(
        mapping = aes(mappings), stat = stat, position = position
      ) + coordinate_function + facet_function + scale_function + theme_function

  - Everything after `geom_function()` is always optional
- `qplot(x =, y =, data =, geom =)` creates complete plot with given parameters
- `last_plot()` returns the most recent plot
- `ggsave("plot_name.png", width = , height =)` saves the last plot in the working directory; file extension included in the name will determine the type of file saved

### Geoms

- Use a geom function to represent data points, use geom's aesthetic properties to represent variables; each function returns a layer
  - *Graphical primitives:*
    > let `a <- ggplot(data, aes(x, y))`
    - `a + geom_blank()` - useful for expanding limits
    - `a + geom_curve(aes(yend = , xend = , curvature = ))` - other properties include `alpha`, `angle`, `color`, `linetype`, `size`
    - `a + geom_path(lineend = , linejoin = , linemitre = )` - other properties include `alpha`, `color`, `group`, `linetype`, `size`
    - `a + geom_polygon(aes(group = ))` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`
    - `a + geom_rect(aes(xmin = , ymin = , xmax = , ymax = ))` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`
    - `a + geom_ribbon(aes(ymin = , ymax = ))` - other properties include `alpha`, `color`, `fill`, `group`, `linetype`, `size`
  - *Line segments:*
    > common aesthetics include `x`, `y`, `alpha`, `color`, `linetype`, `size`  
    > let `a <- ggplot(data, aes(x, y))`
    - `a + geom_abline(aes(intercept = , slope =))`
    - `a + geom_hline(aes(yintercept = ))`
    - `a + geom_vline(aes(xintercept = ))`
      - Other arguments include `lwd` (linewidth) and `color`
    - `a + geom_segment(aes(yend= , xend = ))`
    - `a + geom_spoke(aes(angles= , radius = ))`
  - *One variable, continuous:*
    > let `a <- ggplot(data, aes(x))`
    - `a + geom_area(stat = "bin")` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`
    - `a + geom_density(kernel = "")` - other properties include `alpha`, `color`, `fill`, `group`, `linetype`, `size`, `weight`
    - `a + geom_dotplot()` - properties include `alpha`, `color`, `fill`
    - `a + geom_freqpoly()` - properties include `alpha`, `color`, `group`, `linetype`, `size`
    - `a + geom_histogram(bindwidth = )` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`, `weight`
    - `a + geom_qq(aes(sample = ))` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`, `weight`
  - *One variable, discrete:*
    > let `a <- ggplot(data, aes(x))`
    - `a + geom_bar()` - properties include `alpha`, `color`, `fill`, `linetype`, `size`, `weight`
  - Two variables, both continuous:
    > let `a <- ggplot(data, aes(x, y))`
    - `a + geom_label(aes(label = ), nudge_x = , nudge_y = , check_overlap = TRUE)` - other properties include `alpha`, `angle`, `color`, `family`, `fontface`, `hjust`, `vjust`, `lineheight`, `size`
    - `a + geom_jitter(height = , width = )` - other properties include `alpha`, `color`, `fill`, `shape`, `size`
    - `a + geom_point()` - properties include `alpha`, `color`, `fill`, `shape`, `size`, `stroke`
    - `a + geom_quantile()` - properties include `alpha`, `color`, `group`, `linetype`, `size`, `weight`
    - `a + geom_rug(sides = )` - other properties include `alpha`, `color`, `linetype`, `size`
    - `a + geom_smooth(method = )` - other properties include `alpha`, `color`, `fill`, `group`, `linetype`, `size`, `weight`
    - `a + geom_text(aes(label = ), nudge_x = , nudge_y = , check_overlap = TRUE)` - other properties include `label`, `alpha`, `angle`, `color`, `family`, `fontface`, `jhust`, `vjust`, `lineheight`, `size`
    - `a + geom_bin2d(bindwidth = c(,))` - other properties include `alpha`, `color`, `fill`, `linetype`, `size`, `weight`
    - `a + geom_density2d()` - properties include `alpha`, `color`, `group`, `linetype`, `size`
    - `a + geom_hex()` - properties include `alpha`, `folor`, `fill`, `size`
    - `a + geom_area()` - properties include `alpha`, `color`, `fill`, `linetype`, `size`
    - `a + geom_line()` - properties include `alpha`, `color`, `group`, `linetype`, `size`
    - `a + geom_step(direction = )` - other properties include `alpha`, `color`, `group`, `linetype`, `size`
  - *Two variables, x discrete, y continuous:*
    > let `a <- ggplot(data, aes(x, y))`
    - `a + geom_col()` - properties include `alpha`, `color`, `fill`, `group`, `linetype`, `size`
    - `a + geom_boxplot()` - properties include `lower`, `middle`, `upper`, `ymax`, `ymin`, `alpha`, `color`, `fill`, `group`, `linetype`, `shape`, `size`, `weight`
    - `a + geom_dotplot(binaxis = "y", stackdir = "center")` - other properties include `alpha`, `color`, `fill`, `group`
    - `a + geom_violin(scale = "")` - other properties include `alpha`, `color`, `fill`, `group`, `linetype`, `size`, `weight`
  - *Two variables, both discrete:*
    > let a <- ggplot(data, aes(x, y))}
    - `a + geom_count()` - properties include `alpha`, `color`, `fill`, `shape`, `size`, `stroke`
  - More complicated examples of visualizing error, maps, and three variables available with mathnotes image files at file:///C:/Users/Jake%20Russett/OneDrive/Pictures
  - Potential `geom` aesthetic parameters (usually for color):
    - `fill`
    - `color`
    - `group` (pass factor variable as argument, will create new plot for each level of that factor)

### Stats

- Stats are alternative ways to build layers to plots
  - Visualize stat by changing default stat inside a geom function (i.e. `geom_bar(stat="count")`) or by using stat function (i.e. `stat_count(geom="bar")`)
  - Stat functions include:
    - `stat_bin(binwidth = , origin = )` - other properties include `count`, `ncount`, `density`, `ndensity`
    - `stat_count(width = )` - other properties include `count`, `prop`
    - `stat_density(adjust = , kernel = "")` - other properties include `count`, `density`, `scaled`
    - `stat_bin_2d(bins = , drop = )`
    - `stat_bin_hex(bins = )` - other properties include `count`, `density`
    - `stat_density_2d(contour = , n = )` - other properties include `level`
    - `stat_ellipse(level = , segments = , type = "")`
    - `stat_contour(aes(z = ), )` - other properties include `order`, `level`
    - `stat_summary_hex(aes(z = ), bins = , fun = )` - other properties include `fill`, `value`
    - `stat_summary_2d(aes(z = ), bins = , fun = )` - other properties include `fill`, `value`
    - `stat_boxplot(coef = )` - other properties include `lower`, `middle`, `upper`, `width`, `ymin`, `ymax`
    - `stat_ydensity(kernel = "", scale = "")` - other properties include `density`, `scaled`, `count`, `n`, `violinwidth`, `width`
    - `stat_ecdf(n = )`
    - `stat_quantile(quantiles = c(), formula = , method = "")` - other properties include `quantile`
    - `stat_smooth(method = , formula = , se = , level = )`
    - `stat_function(aes(x = ), n = , fun = , dnorm = , args = list(sd = ))`
    - `stat_identity(na.rm = )`
    - `stat_qq(aes(sample = ), dist = , dparam = list(df = ))` - other properties include `sample`, `theoretical`
    - `stat_sum()` - properties include `size`, `n`, `prop`
    - `stat_summary(fun.data = "")`
    - `stat_summary_bin(fun.y = "", geom = "")`
    - `stat_unique()`

### Scales

- Scales map data values to visual values of an aesthetic
  - Format elements include: scale, aesthetic to adjust, prepackaged scale to use, range of values to include in mapping, scale-specific arguments, title to use in legend/axis, labels to use in legend/axis, breaks to use in legend/axis
  - Example:

        ggplot_graph_object + scale_fill_manual(
            values = c("", "", ...),
            limits = c("", "", ...),
            breaks = c("", "", ...),
            name = "", labels = c("", "", ...)
        )

  - General purpose scales: (can use with most aesthetics; `color`, `fill`, etc.)
    - `scale_aesthetic_continuous()` - map continuous values to visual ones
    - `scale_aesthetic_discrete()` - map discrete values to visual ones
    - `scale_aesthetic_identity()` - map data values as visual ones
    - `scale_aesthetic_manual(values = c())` - map discrete values to manually chosen visual ones
    - `scale_aesthetic_date(date_labels = "%m/%d", date_breaks = "")` - map data values as dates
    - `scale_aesthetic_datetime()` - map data x values as date times; use same arguments as `scale_x_date()` (use command `?strptime` for label formats)
  - X & Y location scales: (use with x or y aesthetics)
    - `scale_x_log10()` - plot x on log10 scale
    - `scale_x_reverse()` - reverse direction of x axis
    - `scale_x_sqrt()` - plot x on square root scale
  - Discrete color and fill scales:
    - `scale_fill_brewer(palette = "")` - for palette choices use command `RColorBrewer::display.brewer.all()`
    - `scale_fill_gray(start = , end = , na.value = "")`
  - Continuous color and fill scales:
    - `scale_fill_distiller(palette = "")`
    - `scale_fill_gradient(low = "", high = "")`
    - `scale_fill_gradient2(low = "", high = "", mid = "", midpoint = )`
    - `scale_fill_gradientn(colors = )`
  - Shape and scale sizes:
    - `scale_shape()`
    - `scale_size()`
    - `scale_shape_manual(values = c())`
    - `scale_radius(range = c())`
    - `scale_size_area(max_size = )`

### Coordinate systems

- `coord_cartesian(xlim = c())` - default cartesian coordinate system
- `coord_fixed(ratio = )` - cartesian coordinates with fixed aspect ratio between x and y units
- `coord_flip()` - flipped cartesian coordinates
- `coord_polar(theta = "", direction = )` - polar coordinates (other properties include start)
- `coord_trans(ytrans = "")` - transformed cartesian coordinates; set `xtrans` and `ytrans` to name of a window function (other properties include `limx`, `limy`, `xtrans`)
- `coord_quickmap()`
- `coord_map(projection = "", orientation = c())` - map projections from `mapproj` package (other properties include `xlim`, `ylim`)

### Position adjustments

- Position adjustments determine how to arrange geoms that would otherwise occupy the same space
  - Set the position parameter inside any geom function to one of the following adjustment values:
    - `"dodge"`
    - `"fill"`
    - `"jitter"`
    - `"nudge"`
    - `"stack"`
  - Each one can also be recast as function with manual width & height arguments; i.e. instead of `position="dodge"`, use `position_dodge(width = , height = )` as a parameter in a geom function

### Themes

- Themes change the visual theme of a plot
  - `theme_bw()`
  - `theme_gray()`
  - `theme_dark()`
  - `theme_classic()`
  - `theme_light()`
  - `theme_linedraw()`
  - `theme_minimal()`
  - `theme_void()`

### Faceting

- Faceting divides a plot into subplots based on values of one or more discrete variables
  - `facet_grid(cols = vars(), rows = vars())` - facet into rows and columns based on variable passed to `vars()` functions
  - `facet_wrap(vars())` - wrap facets into rectangular layout based on variable passed to `vars()` function
    - Can set scales to let axis limits vary across facets
    - Scales parameter can be set to `"free"`, `"free_x"`, `"free_y"`
    - Optionally pass `ncol =` or `nrow =` arguments

### Labels

- All labels are put inside `labs()` function:
  - `x`
  - `y`
  - `title`
  - `subtitle`
  - `caption`
  - `color`

### Legends

- Add legends to a plot
  - `theme(legend.position = "")` - options are `bottom`, `top`, `left`, or `right`
  - `guides(fill = "")` - set legend type for each aesthetic: `colorbar`, `legend`, or `none`
  - `scale_fill_discrete(name = "", labels = c("", "", ...))` - set legend title and labels with scale function

### Zoom

- Zooming with or without clipping
  - `coord_cartesian(xlim = c(), ylim = c())` - without clipping
  - `xlim(), ylim()` - with clipping
  - `scale_x_continuous(limits = c())` - with clipping
  - `scale_y_continuous(limits = c())` - with clipping
