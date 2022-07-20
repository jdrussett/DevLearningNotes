# Plotly Package

## Misc

---

- `Library(plotly)` will instantiate
- `packageVersion('plotly')` checks current version of plotly on your machine
- `plot_ly(x, y)` function defines plotly graph space
  - `x` and `y` are column vectors of numeric values
- `api_create()` actually creates a plotly graph
  - Syntax: `api_create(plot_ly(x, y))` or something like that
  - Specify the `filename=` parameter when using `api_create()` to name the plot something unique so you don't accidentally overwrite it

## YouTube Playlist - Learn Plotly

---

- Plotly - "a must-know tool for building visualizations"
  - Export visualizations to the Plotly Cloud
  - Run visualizations in the browser
  - Interact with Javascript
  - Build with Dash -> web-based Python interface
  - Run plots offline in Jupyter

### Video 1 - Installation & Setup

- Import with anaconda
- Download Anaconda at [https://www.anaconda.com/download](https://www.anaconda.com/download)
  - *Windows must use anaconda prompt for subsequent commands*
- Launch anaconda navigator
  - **Windows**: shortcut tile, or anaconda prompt: anaconda-navigator
  - **Mac/Linux**: command prompt: anaconda-navigator
- Open anaconda navigator & create new environment for plotly
  - Name it `plotly_env` or something
- Activate environment:
  - **Windows**: `command: activate plotly_env`
  - **Mac/Linux**: `source activate plotly_env`
- Download plotly:
  - `conda install -c plotly plotly`
  - Have to install for every environment using it in
- Open jupyter notebook:
  - `jupyter-notebook`
  - Or launch using anaconda navigator UI
- Have to import plotly to notebook to use
  - Command:

            import plotly
            from plotly import __version__ (# statement just to check version)
            print (__version__)
            from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot (# specify tools using from plotly import)

- Setup jupyter notebook:
  - `init_notebook_mode(connected=True)` (# sets up display to render in the jupyter notebook; instead of new browser window/tab; if we don't do this plotly will load as a local url file, like Rstudio would (?))
- Call a plot in jupyter notebook:
  - Command is `iplot()`
  - Example: pass a list of a single dictionary, "x" being equal to list of values and "y" being equal to list of values
- Install additional package: `numpy`
  - From conda prompt: `conda install -c anaconda numpy`
- Create a heat map:
  - `Import plotly.graph_objs and numpy`, with optional aliases
  - Declare x and y as variables both equal to `numpy.random.randn(2000)`
  - Run iplot function:

            iplot([graph_objs.Histogram2Contour(x=x, y=y, contours=dict(coloring='heatmap')), graph_objs.Scatter(x=x, y=y, mode='markers', marker=dict(color='white', size=3, opacity=0.3))], show_link=False)

- Plotly graphs use graph_objs library:
  - Plotly charts described declaratively with objects in `plotly.graph_objs`
  - Every aspect of a plotly chart has a key value in `plotly.graph_objs`
- Install `chart-studio` package for more graph capability
  - `conda install -c plotly chart-studio`
- Import `chart_studio.plotly` and `plotly.graph_objs` with optional aliases
- '**Trace**' is name given to collection of data along with specifications of data in plotly
  - `trace = graph_objs.Scatter(x=numpy.random.rand(N), y=numpy.random.rand(N), mode='markers')`
- Set data variable equal to list containing single element of trace variable defined above
- Run `iplot()` function calling data variable directly
  - `iplot()` function takes argument of a list(s); data is already defined as a list!
- `graph_objs` package in plotly contains lots of plot options
  - See all options at [https://plot.ly/python/reference/](https://plot.ly/python/reference/)
- Define a plot frame/skeleton with `graph_objs.Scatter`, or `graph_objs.Histogram2dContour`, or `graph_objs.Pie`, or whatever
- Create lists/dictionaries/sets as you would in Python (because it's Python)
- `pandas` package contains data import/manipulation tools
- Import a csv dataset with command `pandas.read_csv("[file_path]")`
  - Note: file path must start with `"C:/Users/"` and must use backslashes `/`, not forward slashes `\`
- Combine data and a layout with a `graph_objs.Figure()` object
