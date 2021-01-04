# Interactive Visualizatin in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.


## Lab Goals

## Acknowledgements

The author consulted the following resources when writing  this tutorial:
- Chapter 4.14 "Visualization With Seaborn" from Jake VanderPlas, [*Python Data Science Handbook: Essential Tools for Working with Data*](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html ) (O'Reilly, 2016)
- `pandas`, [User Guide, "Visualization"](https://pandas.pydata.org/docs/user_guide/visualization.html)
- `pandas`, [Getting Started, "Plotting"](https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html)
- Chapter 9 "Plotting and Visualization" from Wes McKinney, [*Python for Data Analysis: Data Wrangling With pandas, Numpy, and IPython*](https://www.oreilly.com/library/view/python-for-data/9781491957653/) (O'Reilly, 2017)
- Chapter 15 "Generating Data" from Eric Matthes, [*Python Crash Course: A Hands-On, Project-Based Introduction to Programming*](https://ehmatthes.github.io/pcc/) (No Starch Press, 2019).
- [`seaborn` package documentation](https://seaborn.pydata.org/introduction.html)
- [`plotly` documentation and tutorials](https://plotly.com/python/)
- [`dash` documentation and tutorials](https://dash.plotly.com/)

# Table of Contents

## Condensed Table of Contents


- [`pandas` and `matplotlib`](#pandas-and-matplotlib)
  * [Plotting in `pandas`Uusing `.plot()`](#plotting-in-pandas-using-plot)
    * [Time Series Data and Line Plots](#time-series-data-and-line-plots)
    * [Bar Charts](#bar-charts)
      * [Grouped Bar Charts](#grouped-bar-charts)
      * [Stacked Bar Charts](#stacked-bar-charts)
      * [Horizontal Bar Charts](#horizontal-bar-charts)
    * [Histograms](#histograms)
    * [Box Plots](#box-plots)
    * [Area Plots](#area-plots)
    * [Scatter Plots](#scatter-plots)
    * [Pie Charts](#pie-charts)
  * [`.plot()` and Missing Data](#plot-and-missing-data)
- [Working with `pandas` and `seaborn`](#working-with-pandas-and-seaborn)
- [Interactive Visualization in Python](#interactive-visualization-in-python)
  * [`bokeh`](#bokeh)
  * [`plotly`](#plotly)
  * [`bokeh` vs. `plotly`](#bokeh-vs-plotly)
- [Getting Started With `plotly`](#getting-started-with-plotly)
  * [The Mechanics of `plotly`](#the-mechanics-of-plotly)
  * [`plotly.express`](#plotlyexpress)
    * [Scatter Plots](#scatter-plots)
    * [Line Plots](#line-plots)
    * [Bar Charts](#bar-charts)
    * [Pie Charts](#pie-charts)
    * [Bubble Charts](#bubble-charts)
    * [Plotting Categorical Data](#plotting-categorical-data)
    * [Maps](#maps)
    * [Tables](#tables)
    * [Additional Plot Types and Resources](#additional-plot-types-and-resources)
  * [Exporting from `plotly`](#exporting-from-plotly)
    * [Static Image Export](#static-image-export)
    * [Saving to HTML](#saving-to-html)
- [`dash`](#dash)
  * [Basic `dash` Syntax](#basic-dash-syntax)
  * [Customizing `dash` Layout with `dash_html_components`](#customizing-dash-layout-with-dash-html-components)
  * [Customizing `dash` Layoout with `dash_core_components`](#customizing-dash-layout-with-dash-core-components)
  * [Setting Up Callbacks](#setting-up-callbacks)
  * [Additional Resources](#additional-resources)
- [Practice Problems](#practice-problems)
- [Lab Notebook Questions](#lab-notebook-questions)

## Detailed Table of Contents

- [`pandas` and `matplotlib`](#pandas-and-matplotlib)
  * [Plotting in `pandas`Uusing `.plot()`](#plotting-in-pandas-using-plot)
    * [Time Series Data and Line Plots](#time-series-data-and-line-plots)
    * [Bar Charts](#bar-charts)
      * [Grouped Bar Charts](#grouped-bar-charts)
      * [Stacked Bar Charts](#stacked-bar-charts)
      * [Horizontal Bar Charts](#horizontal-bar-charts)
    * [Histograms](#histograms)
    * [Box Plots](#box-plots)
    * [Area Plots](#area-plots)
    * [Scatter Plots](#scatter-plots)
    * [Pie Charts](#pie-charts)
  * [`.plot()` and Missing Data](#plot-and-missing-data)
- [Working with `pandas` and `seaborn`](#working-with-pandas-and-seaborn)
- [Interactive Visualization in Python](#interactive-visualization-in-python)
  * [`bokeh`](#bokeh)
  * [`plotly`](#plotly)
  * [`bokeh` vs. `plotly`](#bokeh-vs-plotly)
- [Getting Started With `plotly`](#getting-started-with-plotly)
  * [The Mechanics of `plotly`](#the-mechanics-of-plotly)
  * [`plotly.express`](#plotlyexpress)
    * [Scatter Plots](#scatter-plots)
    * [Line Plots](#line-plots)
    * [Bar Charts](#bar-charts)
    * [Pie Charts](#pie-charts)
      * [Donut Charts](#donut-charts)
      * [Sunburst Charts](#sunburst-charts)
    * [Bubble Charts](#bubble-charts)
    * [Plotting Categorical Data](#plotting-categorical-data)
    * [Maps](#maps)
      * [Geo Maps](#geo-maps)
      * [Mapbox and Tile-Based Maps](#mapbox-and-tile-based-maps)
    * [Tables](#tables)
    * [Additional Plot Types and Resources](#additional-plot-types-and-resources)
  * [Exporting from `plotly`](#exporting-from-plotly)
    * [Static Image Export](#static-image-export)
    * [Saving to HTML](#saving-to-html)
- [`dash`](#dash)
  * [Basic `dash` Syntax](#basic-dash-syntax)
  * [Customizing `dash` Layout with `dash_html_components`](#customizing-dash-layout-with-dash-html-components)
  * [Customizing `dash` Layoout with `dash_core_components`](#customizing-dash-layout-with-dash-core-components)
    * [Dropdown](#dropdown)
    * [Slider](#slider)
    * [RangeSlider](#rangeslider)
    * [Input](#input)
    * [TextArea](#textarea)
    * [Checkboxes](#checkboxes)
    * [Other Core Component Types](#other-core-component-types)
  * [Setting Up Callbacks](#setting-up-callbacks)
  * [Additional Resources](#additional-resources)
- [Practice Problems](#practice-problems)
- [Lab Notebook Questions](#lab-notebook-questions)

# `pandas` and `matplotlib`

Having to load data manually to build a visualization or plot gets cumbersome quickly.

In many situations, we might want to work with data in a `pandas` `DataFrame` when building a visualization.

`pandas` includes a `.plot()` attribute that interacts with the `matplotlib` API to generate plots.

The `pandas` `.plot()` attribute relies on the `matplotlib` API to generate plots, so our work with `matplotlib` will come in handy when we need to customize plots generated using `.plot()`.

And in many cases, the `.plot()` syntax is similar to `matplotlib` `OO` syntax.

## Plotting in `pandas` Using `.plot()`

Let's go back to the air quality data we were working with previously in `pandas`.

To load the data as a dataframe:
```Python
# import pandas
import pandas as pd

# load data from url to dataframe
air_quality = pd.read_csv('https://raw.githubusercontent.com/pandas-dev/pandas/master/doc/data/air_quality_no2.csv', index_col=0, parse_dates=True)

# check data has loaded
air_quality.head()
```

We can do a quick visual check of the data by passing the entire data frame to `.plot()`.
```Python
# import matplotlib
import matplotlib.pyplot as plt

# generate plot
air_quality.plot()

# show plot
plt.show()
```

This isn't a particularly meaningful visualization, but it shows us how the default for `.plot()` creates a line for each column with numeric data.

The index is used for the `X` axis, and all numeric columns are plotted on the `Y` axis.

We can also see that `.plot()` pulls tick marks, tick labels, and axis titles from the underlying `dataframe`.

Let's say we only wanted to plot Paris data.

We can select that column in the `dataframe` before calling `.plot()`.
```Python
air_quality["station_paris"].plot()
```

We can plot a specific column in the `dataframe` using the `[" "]` selection method.

Let's say we want to visually compare NO<sub>2</sub> values measured in London and Paris.

We need to specify what column is going to be used for the `X` axis as well as what column is going to be used for the `Y` axis.

For this example, a scatterplot will be more effective than a lineplot.

We can create a scatterplot using `.plot.scatter()`.

```Python
air_quality.plot.scatter(x="station_london", y="station_paris", alpha=0.5)
```

This example generates a scatterplot with London data on the `X` axis and Paris data on the `Y` axis.

While the default for `.plot()` is a lineplot, there are a number of other methods we can use with `.plot()`.

Again, you will see some overlap with `matplotlib` syntax.

We can use these strings as as method in combination with `.plot()` or we can pass them to `.plot()` as a `kind` parameter.

Plot Type | Method Syntax | Parameter Syntax
--- | --- | ---
Default (line) | `.plot()` | NA
Area | `.plot.area()` | `.plot(kind='area')`
Bar | `.plot.bar()` | `.plot(kind='bar')`
Horizontal bar | `.plot.barh()` | `.plot(kind='barh')`
Box | `.plot.box()` | `.plot(kind='box')`
Density | `.plot.density()` | `.plot(kind='density')`
Hexbin | `.plot.hexbin()` | `.plot(kind='hexbin')`
Histogram | `.plot.hist()` | `.plot(kind='hist')`
Kernel density | `.plot.kde()` | `.plot(kind='hist')`
Line | `.plot.line()` | `.plot(kind='line')` *this would be redundant since the default for `.plot()` is line*
Pie | `.plot.pie()` | `.plot(kind='pie')`
Scatter | `.plot.scatter()` | `.plot(kind='scatter')`

In general, it's more effective to use the method syntax to note plot type, rather than treating plot type as a parameter.

Let's create a box plot using our air quality data.
```Python
air_quality.plot.box()
```

We can see each numeric column (each station) has its own box in the default boxplot.

Let's say we wanted to generate a lineplot with separate subplots for each of the numeric columns.

We can accomplish this by setting the `subplots` parameter to `True`.

```Python
axs = air_quality.plot.area(figsize=(12, 4), subplots=True)
```

Let's say we want to further customize this plot.

This is where we start to see more `matplotlib` syntax in play.

```Python
# create figure and axes
fig, axs = plt.subplots(figsize=(12, 4))

# build area plot
air_quality.plot.area(ax=axs)

# set y axis label
axs.set_ylabel("NO$_2$ concentration")

# save plot as png file
fig.savefig("no2_concentrations.png")
```

Each plot object created by `pandas` is also a `matplotlib` object.

Having a deep knowledge of `matplotlib` allows you to customize plots generated using `pandas` `.plot()` function.

That said, there are some parameters you can set as part of `.plot()` without having to have separate `matplotlib` syntax commands.

The plot `kind` is one parameter option, as is the `dataframe`, `X` axis data, and `Y` axis data.

Other parameters:

Parameter | Explanation
--- | ---
`ax` | `matplotlib` `axes` object; axes for the current figure
`subplots` | Default is `False`; set to `True` to enable multiple plots in the same figure
`layout` | Follows `(rows, columns)` syntax to set subplot layout
`figsize` | Follows `(width, height)` syntax; Sets figure object width and height in inches
`use_Index` | Default is `True`; uses dataframe index as ticks for `X` axis
`title` | Title to use for the plot; can take a list with titles for corresponding subplots
`grid` | Default is `False`; set to `True` to show axis grid lines
`legend` | Places legend on axis subplot
`xticks` | Values to use for `X` axis ticks
`yticks` | Values to use for `Y` axis ticks
`xlim` | Follows `(lower limit, upper limit)` syntax; Sets `X` axis limits
`ylim` | Follows `(lower limit, upper limit)` syntax; Sets `Y` axis limits
`xlabel` | Label for `X` axis; default uses index column name
`ylabel` | Label for `Y` axis; default uses `Y` column name
`fontsize` | Sets font size for tickmarks
`colormap` | Sets `matplotlib` colormap to select colors from
`table` | Default is `False`; set to `True` to draw a table from data in the `DataFrame`
`stacked` | Default is `False` in line and bar plots, `True` in area plot; if `True`, creates stacked plot

For more parameters that can be passed to `.plot()`: [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)

Let's walk through a few more examples of using `.plot()` with a `pandas` `DataFrame`.

NOTE: The `.plot()` method can be used on `pandas` `Series` and `DataFrame`. These examples focus on `DataFrame`s.

### Time Series Data and Line Plots

Let's generate some random time series data.
```Python
# import pandas
import pandas as pd

# import matplotlib
import matplotlib.pyplot as plt

# import numpy
import numpy as np

# create series with random numbers organized over time series
ts = pd.Series(np.random.randn(1000), index=pd.date_range("1/1/2000", periods=1000))

# cumulative sum calculated by iterating over Series
ts = ts.cumsum()

# generate line plot
ts.plot()
```

In this example, our `Series` index labels are specified using `pd.date_range()`.

These are the `X` axis values.

The index values are the 1000 random values generated by `np.random.randn()`.

We use the cumulative sum `.cumsum` to determine the total value for each unique time in the series.

Let's modify this example to use a `DataFrame`.
```Python
# create new dataframe with random numbers, the original time series index, and four columns
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index, columns=list("ABCD"))

# calculate cumulative sum
df = df.cumsum()

# create figure
plt.figure()

# create plot
df.plot()
```

#### Additional Resources

For more on line plots:
- [`pandas`, "Basic plotting"](https://pandas.pydata.org/docs/user_guide/visualization.html#basic-plotting-plot)
- [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)
- [`pandas.DataFrame.plot.line`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.line.html)

### Bar charts

Let's say we want to create a bar chart with a single line of data from our `df` `DataFrame`.

We can select a specific row using `iloc`.

```Python
# create figure
plt.figure()

# create bar plot for single row of data
df.iloc[5].plot.bar()

# show plot
plt.show()
```

#### Grouped bar chrat

Let's say we want to produce a grouped bar chart.

We can create a `DataFrame` with four columns and random values.

```Python
# create dataframe
df2 = pd.DataFrame(np.random.randn(10, 4), columns=['a', 'b', 'c', 'd'])

# generate bar chart
df2.plot.bar()
```

By default, `.plot.bar()` creates a separate bar for each of the numeric columns.

We could select a single column using `['']` to only show one bar or column value.

#### Stacked bar chart

If we wanted to show this data as a stacked bar chart, we would set the `stacked` parameter to `True`.
```Python
df2.plot.bar(stacked=True)
```

#### Horizontal bar chart

Remember `.plot.barh()` generates a horizontal bar chart, and we can also set `stacked` to `True` here to create a horizontal stacked bar chart.
```Python
df2.plot.barh(stacked=True)
```

#### Additional Resources

For more on bar charts:
- [`pandas`, "Bar plots"](https://pandas.pydata.org/docs/user_guide/visualization.html#bar-plots)
- [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)
- [`pandas.DataFrame.plot.bar`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.bar.html)
- [`pandas.DataFrame.plot.barh`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.barh.html)

### Histograms

The `.plot.hist()` method will generate a histogram.

We can also use `.hist()` to generate a histogram.

```Python
# create dataframe with three columns using dictionary with random number data
df = pd.DataFrame({"a": np.random.randn(1000) + 1, "b": np.random.randn(1000), "c": np.random.randn(1000) - 1,}, columns=["a", "b", "c"],)

# create figure object
plt.figure()

# create histogram
df4.plot.hist(alpha=0.5)
```

We can set `stacked` to `True` to create a stacked histogram.
```Python
df4.hist(stacked=True)
```

We can also specify the bin size using the `bins` keyword.
```Python
df4.plot.hist(bins=20)
```

We can use the `.hist()` method in `matplotlib` to further customize our histogram: [`matplotlib.axes.Axes.hist`](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.hist.html#matplotlib.axes.Axes.hist)

#### Additional Resources

For more on histograms:
- [`pandas`, "Visualization, Histograms"](https://pandas.pydata.org/docs/user_guide/visualization.html#visualization-hist)
- [`pandas.DataFrame.plot.hist`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.hist.html)
- [`pandas.DataFrame.hist`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.hist.html)

#### Box plots

We can generate box plots using `.plot.box()` or `.boxplot()`.

The default settings visualize the distribution of values within each column.

Back to our random number dataframe, this time with five columns.

```Python
# create dataframe
df = pd.DataFrame(np.random.randn(10, 5), columns=['A', 'B', 'C', 'D', 'E'])

# create plot
df.plot.box()
```

We can add colors to our box plot using the `color` keyword.
```Python
df.plot.box(color='blue')
```

We can also use a dictionary with key-value pairs for each component of our box plot.
```Python
# set color dictionary
color = {"boxes": "DarkGreen", "whiskers": "DarkOrange", "medians": "DarkBlue", "caps": "Gray",}

# draw plot and specify colors and outlier symbol using keyword argument or kwarg
```Python
df.plot.box(color=color, sym="r+")
```

#### Additional Resources

For more on box plots:
- [`pandas`, "Visualization, Box plots"](https://pandas.pydata.org/docs/user_guide/visualization.html#box-plots)
- [`pandas.DataFrame.plot.box`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.box.html)
- [`pandas.DataFrame.boxplot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.boxplot.html)

### Area Plots

Basic syntax:
```Python
df = pd.DataFrame(np.random.randn(10, 4), columns=["a", "b", "c", "d"])

df.plot.area()
```

For more on area plots:
- [`pandas`, "Visualization, Area plot"](https://pandas.pydata.org/docs/user_guide/visualization.html#area-plot)
- [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)
- [`pandas.DataFrame.plot.area`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.area.html)

### Scatter Plots

Basic syntax:
```Python
df = pd.DataFrame(np.random.rand(50, 4), columns=["a", "b", "c", "d"])

df.plot.scatter(x="a", y="b")
```

For more on scatter plots:
- [`pandas`, "Visualization, Scatter plot"](https://pandas.pydata.org/docs/user_guide/visualization.html#scatter-plot)
- [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)
- [`pandas.DataFrame.plot.scatter`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.scatter.html)

### Pie Plots

Basic syntax:
```Python
series = pd.Series(3 * np.random.rand(4), index=["a", "b", "c", "d"], name="series")

series.plot.pie(figsize=(6, 6))
```

For more on pie plots:
- [`pandas`, "Visualization, Scatter plot"](https://pandas.pydata.org/docs/user_guide/visualization.html#scatter-plot)
- [`pandas.DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.html)
- [`pandas.DataFrame.plot.scatter`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.plot.scatter.html)

## `.plot()` and missing data

Just like `pandas` has built-in settings for handling missing data or `NaN` values, the `.plot()` method also has default settings for how each type of plot handles missing data.

Plot Type | NaN Handling 
--- | ---
Line | Leaves gaps
Stacked line | Fills 0s
Bar | Fills 0s
Scatter | Drops missing values
Histogram | Drops missing values (column-wise)
Box | Drops missing values (column-wise)
Area | Fills 0s
Kernel density (KDE) | Drops missing values (column-wise)
Hexbin | Drops missing values
Pie | Fills 0s

To customize or alter these default settings, you would use `.fillna()` or `.dropna()` to filter the `DataFrame` before generating the plot.

## Additional resources

For more on plotting with `pandas` and `matplotlib`:
- [`pandas`, Tutorials, "Plotting"](https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html)
- [`pandas`, "Plotting tools"](https://pandas.pydata.org/docs/user_guide/visualization.html#plotting-tools)
- [`pandas`, "Plot formatting"](https://pandas.pydata.org/docs/user_guide/visualization.html#plot-formatting)
- [`pandas`, "Plotting directly with matplotlib"](https://pandas.pydata.org/docs/user_guide/visualization.html#plotting-directly-with-matplotlib)

# Working with `pandas` and `seaborn`

As we've covered previously, `matplotlib` gives you a wide range of base components to work with when generating plots.

But, `matplotlib` does have limitations, and building a plot from the ground up, specifying each component can be cumbersome (and result in significant boilerplate code).

Advanced statistical analysis with `matplotlib` is possible, but cumbersome.

If you need to engage in advanced statistical analysis beyond what is easily accessible in `matplotlib`, `seaborn` is a statistical data visualization library that works well with `pandas`.

"`seaborn` is a Python data visualization library based on matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics" (["Seaborn"](https://seaborn.pydata.org/).

`seaborn` works with `numpy`, `scipy`, `pandas`, and `matplotlib` to simply high-level functions for common statistical plots.

Let's compare `seaborn` and `matplotlib` using random walk data and a line plot.

Sample line plot generated using only `matplotlib`:
```Python
# import necessary packages
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# create random walk data
rng = np.random.RandomState(0)
x = np.linspace(0, 10, 500)
y = np.cumsum(rng.randn(500, 6), 0)

# create figure
fig, ax = plt.subplots()

# generate line plot
ax.plot(x, y)

# create legend
ax.legend('ABCDEF', ncol=2, loc='upper left')

# show plot
plt.show()
```

An okay plot, but not particularly effective for this data.

Let's generate the same plot with `seaborn` running on top of `matplotlib`.
```Python
# add seaborn package
import seaborn as sns

# set seaborn  style
sns.set()

# create figure
fig, ax = plt.subplots()

# generate line plot
ax.plot(x, y)

# create legend
ax.legend('ABCDEF', ncol=2, loc='upper left')

# show plot
plt.show()
```

A simple way to incorporate `seaborn` with `matplotlib` is to use `seaborn`'s plot styling.

`matplotlib` also has a few different style sheets based on `seaborn`.

Let's look at a couple more sophisticated statistical plots built using `seaborn`.

We can create a plot that highlights the relationship between resturaunt bill amount, tip, and meal time.

This data comes from the `tips` example dataset already packaged in `seaborn`.
```Python
# import seaborn
import seaborn as sns

# apply default seaborn theme
sns.set_theme()

# load dataset already stored as dataframe
tips = sns.load_dataset("tips")

# create plot
sns.relplot(data=tips, x="total_bill", y="tip", col="time", hue="smoker", style="smoker", size="size",)
```

`seaborn` draws on `matplotlib`, but we don't need to directly load or import `matplotlib`.

We load the `tips` dataset as a `DataFrame`.

We then create a visualization that shows the relationships between the five dataset variables through the single call to the `.relplot()` function.

We can start to think through all of the work happening behind the scenes in `matplotlib` to generate this visualization:
- create figure/axes object with a 2, 1 subplot grid
- create subplots
- set tick values and labels for each axis for both subplots
- set axis labels and plot titles for both subplots
- set plot type for each subplot
- set symbol types, color, and size for each type of datapoint, for each subplot
- generate legend

And the list goes on.

`seaborn` handles all of those translations from the dataframe to `matplotlib` arguments.

This simplifies the work of writing code to generate this plot.

`seaborn`'s `.relplot()` function is designed to visualize statistical relationships.

Sometimes scatterplots are the most effective way to show these relationships.

But, in a relationship where one variable is a measure of time, a line can be a more effective representation.

We can use the `kind` parameter with the `.relplot()` function to make this change.

An example of `.relplot()` using a different sample dataset.
```Python
# load sample dataset as dataframe
dots = sns.load_dataset('dots')

# creat line plot showing relationships
sns.relplot(
    data=dots, kind="line",
    x="time", y="firing_rate", col="align",
    hue="choice", size="coherence", style="choice",
    facet_kws=dict(sharex=False),
)
```

In this example, the `style` parameter impacted line weight and style, rather than marker size as it did in the previous example.

A few other `seaborn` examples.

Relationship plot that presents average of one variable as a function of other variables.
```Python
fmri = sns.load_dataset("fmri")
sns.relplot(
    data=fmri, kind="line",
    x="timepoint", y="signal", col="region",
    hue="event", style="event",
)
```

`seaborn` estimates the statistical values using bootstrapping to compute confidence intervals and draw error bars to show uncertainty.

We could go back to our bill and tip data to generate a scatterplot that includes a linear regression model.
```Python
sns.lmplot(data=tips, x="total_bill", y="tip", col="time", hue="smoker")
```

We can visualize variable distribution with kernel density estimation.
```Python
sns.displot(data=tips, x="total_bill", col="time", kde=True)
```

`seaborn` can also calculate and plot the empirical cumulative distribution function (`ecdf`).
```Python
sns.displot(data=tips, kind="ecdf", x="total_bill", col="time", hue="smoker", rug=True)
```

We can also generate plots that are geared toward categorical data.

A `swarm` plot is a scatterplot with adjusted point positions on the categorical axis to minimize overlap
```Python
sns.catplot(data=tips, kind="swarm", x="day", y="total_bill", hue="smoker")
```

We could also display this categorical data using kernel density estimation and a violin plot.
```Python
sns.catplot(data=tips, kind="violin", x="day", y="total_bill", hue="smoker", split=True)
```

We could also display this data with a grouped bar chart that shows mean values and confidence intervals for each category.
```Python
sns.catplot(data=tips, kind="bar", x="day", y="total_bill", hue="smoker")
```

This is just a taste of how `seaborn` works to generate more advanced statistical plots.

Because the package integrates with `matplotlib`, customizing `seaborn` plots requires knowledge of `matplotlib` functionality and syntax.

Dropping down to the `matplotlib` layer is not always necessary (as shown in these examples), but a robust `matplotlib` foundation is knowledge that transfers when working with `seaborn`.

For more on `seaborn`:
- [`seaborn`, "seaborn: statistical data visualization"](http://seaborn.pydata.org/)
- [`seaborn`, "Installing and getting started"](https://seaborn.pydata.org/installing.html)
- [`seaborn`, "An introduction to seaborn"](http://seaborn.pydata.org/introduction.html)
- [`seaborn`, "User guide and tutorial"](http://seaborn.pydata.org/tutorial.html)
- [`seaborn`, "Example gallery"](https://seaborn.pydata.org/examples/index.html)
- [`seaborn`, "API reference"](https://seaborn.pydata.org/api.html)
- [Jake VanderPlas, "Visualization With Seaborn" from *Python Data Science Handbook*](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html)


# Interactive visualization in Python

Up to this point, we have been generatic static image plots in Python using a combination of `pandas`, `matplotlib`, and `seaborn`.

But in many cases we may want to generate interactive plots that can exist on the web.

We see this type of interactivity in data journalism projects :

We also see this kind of interactivity in dashboard-style interfaces:

The two leading Python packages that can be used to generate interactive visualizations for the web are `bokeh` and `plotly`.

We'll provide a brief overview for each, with some comparison considerations, before focusing on `plotly`.

## `bokeh`

"Bokeh is an interactive visualization library for modern web browsers. It provides elegant, concise construction of versatile graphics, and affords high-performance interactivity over large or streaming datasets. Bokeh can help anyone who would like to quickly and easily make interactive plots, dashboards, and data applications" ([bokeh documentation](https://docs.bokeh.org/en/latest/index.html))

`bokeh` emerged in 2013, and uses a glyph and model based approach when building interactive visualizations.

`bokeh` is built on `D3.js`, a JavaScript library for interactive visualization.

Full customization in `bokeh` requires some knowledge of JavaScript.

FIGURE 1

Sample code and output for a `bokeh` plot.

For more on `bokeh`:
- [`bokeh` documentation](https://docs.bokeh.org/en/latest/index.html#)
- [`bokeh`, Installation](https://docs.bokeh.org/en/latest/docs/installation.html)
- [`bokeh`, User Guide](https://docs.bokeh.org/en/latest/docs/user_guide.html)
- [`bokeh`, Tutorial](htthttps://mybinder.org/v2/gh/bokeh/bokeh-notebooks/7b6da26945e284b19df07daecc6beabdb7adbe81)
- [`bokeh`, Reference](https://docs.bokeh.org/en/latest/docs/reference.html#refguide)
- Charlie Harper, "Visualizing Data with Bokeh and Pandas," *The Programming Historian* 7 (2018), [https://doi.org/10.46430/phen0081](https://doi.org/10.46430/phen0081)

## `plotly`

"Plotly is a technical computing company headquartered in Montreal, Quebec, that develops online data analytics and visualization tools. Plotly provides online graphing, analytics, and statistics tools for individuals and collaboration, as well as scientific graphing libraries for Python, R, MATLAB, Perl, Julia, Arduino, and REST" ([Wikipedia](https://en.wikipedia.org/wiki/Plotly)).

The `plotly` Python graphing library is supported by the Plotly company.

Plotly relies on Python and the Django framework, using JavaScript, D3.js, HTML, and CSS for its front-end.

Plotly files are stored on Amazon Web Services' Simple Storage Service (S3).

The company was founded in 2012 and went on to be a featured startup at 2013 PyCon, sponsoring the SciPy conference in 2018.

During Series A funding, Plotly raised $5.5 million, supported by MHS Capital, Siemens Venture Capital, Rho Ventures, Real Ventures, and Silicon Valley Bank.

Plotly offers a range of products, some of which are free or open-source, and others that are subscription based.
- ***Dash***: an open-source web application framework for Python, R, and Julia
- ***Chart Studio***: a graphical user interface for analyzing and visualizing data; single-user version is free, enterprise deployments have a pricing model
- ***API libraries***: open-source graphing libraries for Python, R, and Julia
- ***Plotly Apps***: Google Chrome app
- ***PLotly.js***: open-source JavaScript graphic and dashboard library
- ***Plotly Enterprise***: pricing model for local Plotly installation and deployment

In recent years, Plotly has moved into machine learning and artificial intelligence app support and artificial intelligence supply chain technology and continues to expand its enterprise pricing options.

For more on Plotly history: [Plotly, "About Us"](https://plotly.com/about-us/)

For more on Plotly products:
- [Dash Enterprise](https://plotly.com/dash/)
- [Consulting and Training](https://plotly.com/consulting-and-oem/)
- [Chart Studio](https://plotly.com/chart-studio/)

Plotly's enterprise products are used by corporations that include NVIDIA, Tesla, Shell, Citi Bank, and Amgen.

Plotly's Chart Studio product is used by a range of journalism outfits and companies, including S&P Global, The Washington Post, Wired, Tesla, and Medium.

At the time this tutorial was written (December 2020), Plotly's senior leadership team has no women in technical roles and no people of color.

## `bokeh` vs. `plotly`

At first glance, `bokeh` and `plotly` appear to have similar features and functionality.

Both are based on JavaScript libraries, can work with data stored in `pandas`, and generate interactive web applications.

The packages have very different syntax for how they build visualizations and applications, and they rely on different back-end infrastructure when deploying web applications.

In addition to having the support and infrastructure of the Plotly company, `plotly` has a significantly larger user community comprised of individuals and corporations.

`plotly` graphing libraries are also available in languages other than Python, most notably R and Julia.

`bokeh` is designed for Python, with the stand-alone BokehJS library available for JavaScript.

This tutorial focuses on `plotly`, but the `bokeh` resources highlighted above are a useful place to start for working with the other package.

For more in-depth `bokeh` and `plotly` comparisons:
- Paul Iacomi, ["Plotly vs. Bokeh: Interactive Python Visualisation Pros and Cons"](https://pauliacomi.com/2020/06/07/plotly-v-bokeh.html) *personal blog* (7 June 2020)
- stackshare, ["Bokeh vs Plotly](https://stackshare.io/stackups/bokeh-vs-plotly)
- Flavian, ["Bokeh vs Dash- Which is the Best Framework for Python?](https://www.sicara.ai/blog/2018-01-30-bokeh-dash-best-dashboard-framework-python) *Sicara* (20 February 2020)
- reddit, ["Plotly vs Bokeh vs..."](https://www.reddit.com/r/Python/comments/5nwk9r/plotly_vs_bokeh_vs/) (2017)
- Scott Fitzpatrick, ["Creating Python Dashboards: Dash Vs Bokeh"](https://www.activestate.com/blog/dash-vs-bokeh/) *Active State* (19 September 2019)
- Gabriela Moreira Mafra, ["Choosing one of many Python visualization tools"](https://blog.magrathealabs.com/choosing-one-of-many-python-visualization-tools-7eb36fa5855f) *Magrathea Lab Blog* (22 September 2018)
- Antoine Hue, ["Which library should I use for my Python dashboard?"](https://towardsdatascience.com/which-library-should-i-use-for-my-dashboard-c432726a52bf) *Towards Data Science* (31 August 2020)

# Getting started with `plotly`

To install `plotly`:
- using `pip`: `pip install plotly`
- using `conda`: `conda install -c plotly`
- using Jupyter Notebook: `pip install "notebook>=5.3" "ipywidgets>=7.2"`
- using `conda` in Jupyter Notebook: `conda install "notebook>=5.3" "ipywidgets>=7.2"`

## The mechanics of `plotly`

Plotly.js, the JavaScript library `plotly` is based on understands figures as trees with named nodes called attributes.

The root node of the tree as three top-level attributes.

The top-level ***`data`*** attribute consists of a lists of dicts referred to as traces.

Each trace has a plot type (scatter, bar, pie, etc.), and is drawn on a single subplot.

Traces can have a single legend, and other attributes depending on trace type.

The top-level ***`layout`*** attribute is referred to as "the layout" and consists of a dict with attributes that control non-data parts of the figure.

Parts of the figure governed by the `layout` attribute include:
- Dimensions and margins
- Templates, fonts, colors, hover labels
- Titles and legends
- Non-data marks such as annotations, shapes, and images
- Controls like buttons, toggles, menus, or sliders

The top-level ***`frames`*** attribute does not exist for all types of plots.

`frames` consists of a list of dicts that define sequential frames in an animated plot.

Each frame in the sequence has its own `data` attribute (and other parameters).

When building a figure, you do not have to populate every attribute of every object.

The JavaScript layer can compute default values for some unspecified attributes.

Let's look at an example for a simple line plot.

Python code that generates the plot using `plotly`:
```Python
# import plotly
import plotly.express as px

# create figure
fig = px.line(x=["a","b","c"], y=[1,3,2], title="sample figure")

# print figure
print(fig)

# show figure
fig.show()
```

The JSON object generated as part of `plotly`'s back-end process:
```JSON
Figure({
    'data': [{'hovertemplate': 'x=%{x}<br>y=%{y}<extra></extra>',
              'legendgroup': '',
              'line': {'color': '#636efa', 'dash': 'solid'},
              'mode': 'lines',
              'name': '',
              'orientation': 'v',
              'showlegend': False,
              'type': 'scatter',
              'x': array(['a', 'b', 'c'], dtype=object),
              'xaxis': 'x',
              'y': array([1, 3, 2]),
              'yaxis': 'y'}],
    'layout': {'legend': {'tracegroupgap': 0},
               'template': '...',
               'title': {'text': 'sample figure'},
               'xaxis': {'anchor': 'y', 'domain': [0.0, 1.0], 'title': {'text': 'x'}},
               'yaxis': {'anchor': 'x', 'domain': [0.0, 1.0], 'title': {'text': 'y'}}}
})
```

We can use `fig.to_dict()` and `fig.to_json()` to represent the back-end of a `plotly` figure as a dictionary or JSON object, respectively.

2D Cartesian coordinate system subplots are the most commonly-used type of subplot.

In `plotly`, traces compatible with these subplots support `xaxis` and `yaxis` attributes.

Trace types compatible with 2D cartesian subplots incldue scatterplots, bar charts, histograms, and box plots.

Both `X` and `Y` axes support a `type` attribute.

The `type` attribute can modify a trace to show continuous values, temporal values, or categorical values.

For more on the figure data structure: [`plotly`, "The Figure Data Structure in Python"](https://plotly.com/python/figure-structure/)

For more on `plotly` fundamental syntax: [Plotly Python Open Source Graphing Library Fundamentals](https://plotly.com/python/plotly-fundamentals/)

## `plotly.express`

The `plotly.express` module contains functions that can create entire figures at once. 

`plotly.express` functions are a designed to be a user-friendly point of entry to the `plotly` package.

A graph object is created as part of any `plotly.express` function, but the point of the `plotly.express` function is to significantly reduce the amount of code needed to create, customize, and render the graph object.

### Scatter Plots

To create a scatterplot using `plotly.express`, we use the `px.scatter()` function, which takes values for the `X` and `Y` axis.

Without any additional arguments, the default formatting and style options are applied.

```Python
# import plotly.express
import plotly.express as px

# create figure 
fig = px.scatter(x=[0, 1, 2, 3, 4], y=[0, 1, 4, 9, 16])

# show figure
fig.show()
```

Everything from tick marks to axis labels to grid lines to hover labels has been generated by the `plotly.express` defaults.

To create a scatterplot from data stored in a `DataFrame`, the same general syntax specifying `X` and `Y` values still applies.

An example using data about flowers.
```Python
# import plotly.express
import plotly.express as px

# load sample data already stored as a dataframe
df = px.data.iris()

# create figure
fig = px.scatter(df, x="sepal_width", y="sepal_length")

# show figure
fig.show()
```

In the `dataframe` example, we passed the entire data frame to `px.scatter()`, and specified with columns to use for the `X` and `Y` axis.

In the resulting figure, we can see how `plotly` assigns the column names as axis labels.

We can modify point color and size to reflect underlying values in the data frame.

We can also modify the information displayed in the hover label.

```Python
# import plotly.express
import plotly.express as px

# load sample data already stored as a dataframe
df = px.data.iris()

# create figure
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species", size="petal_length", hover_data=["petal_width"])

# show figure
fig.show()
```

In this modified example, `color` specifies what field to use to color points.

`size` specifies what field to use to size points.

`hover_data` adds fields not already incorporated in the figure to the hover label, which now includes 5 different fields.

#### Additional resources

For more on scatter plots in `plotly`:
- [`plotly`, Scatter Plots in Python](https://plotly.com/python/line-and-scatter/)
- [`plotly.express.scatter`](https://plotly.com/python-api-reference/generated/plotly.express.scatter)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)
- [`plotly`, Python Figure Reference: `scattergl` Traces](https://plotly.com/python/reference/scattergl/)

### Line Plots

We can create a simple line plot using `px.line()`.

This example uses example data on life expectancy.

```Python
# import plotly
import plotly.express as px

# load dataframe subset 
df = px.data.gapminder().query("country=='Canada'")

# create figure
fig = px.line(df, x="year", y="lifeExp", title='Life expectancy in Canada')

# show figure
fig.show()
```

In this example, we pass a subset of the `gapminder` dataframe to the `px.line()` fucntion.

We specify which fields to use for the `X` and `Y` axis values, and we give the figure a title.

Let's say we wanted to create a line plot with data for two countries.

We could filter the data frame accordingly and use the `color` parameter.

```Python
# import plotly
import plotly.express as px

# load dataframe subset 
df = px.data.gapminder().query("continent=='Oceania'")

# create figure
fig = px.line(df, x="year", y="lifeExp", color='country', title='Life Expectancy by Country')

# show figure
fig.show()
```

Let's say we want to modify the line plot to include a line for individual countries and color the lines by continent.

```Python
# import plotly
import plotly.express as px

# load dataframe subset
df = px.data.gapminder().query("continent !- 'Asia'")

# create figure
fig = px.line(df, x="year", y="lifeExp", color='continent', line_group='country', hover_name='country', title='Country Life Expectancy by Continent')

# show figure
fig.show()
```

In the modified example, we color the lines by continent and group the lines by country.

We also use `line_group` to group rows in a column into lines.

We use `hover_name` to set a title or name for the hover labels.

The country name is now at the top of each over label.

#### Additional resources

For more on line plots in `plotly`:
- [`plotly`, Line Charts in Python](https://plotly.com/python/line-charts/)
- [`plotly.express.line`](https://plotly.com/python-api-reference/generated/plotly.express.line)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)

### Bar Charts

We can create a bar chart using `px.bar()`.

In the default settings, each row of the dataframe is represented as a rectangular mark.

An example using population data from the previous example's dataset.

```Python
# import plotly
import plotly.express as px

# load subset of existing dataframe
data_canada = px.data.gapminder().query("country == 'Canada'")

# create figure
fig = px.bar(data_canada, x='year', y='pop')

# show figure
fig.show()
```

In this example, the `year` column is assiged as the `X` axis value, and the `pop` column is assigned as the `Y` axis value.

We can also generate a stacked bar chart using `px.bar()`.

Let's take a look at a stacked bar chart for sample data stored in two different formats.

As we learned in the `pandas` lab, data can be stored in a long or wide form.

***Long-form data*** has one row per observation and one column per variable. Also known as tidy data.

***Wide-form data*** has one row per value of the first variable, and one column per value of the second value.

A quick comparison of long and wide data for the same Olympic medal dataset.

```Plotly
# import plotly
import plotly.express as px

# create data table from long dataframe
long_df = px.data.medals_long()

# show long data table
long_df
```

```Plotly
# import plotly
import plotly.express as px

# create data table from long dataframe
wide_df = px.data.medals_wide()

# show long data table
wide_df
```

`plotly.express` and `px.bar()` can generate the same plot from either data form.

#### Stacked bar chart

To create a stacked bar chart using the long data form:
```Python
# import plotly
import plotly.express as px

# load dataframe
long_df = px.data.medals_long()

# create figure
fig = px.bar(long_df, x="nation", y="count", color="medal", title="Long-Form Input")

# show figure
fig.show()
```

To create a stacked bar chart using the wide data form:
```Python
# import plotly
import plotly.express as px

# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input")

# show figure
fig.show()
```

In the wide-format example, we pass a list of columns to the `Y` axis.

For the wide-format example, we might want to relabel the fields when generating the hover labels.
```Python
# import plotly
import plotly.express as px

# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input, relabelled", labels={"value": "count", "variable": "medal"})

# show figure
fig.show()
```

In the modified example, we passed a dictionary to `labels` to manually rename those fields in the hover label.

If we wanted to change the styling for the wide-format example, we could specify a style template (similar to a style sheet), a colormap, and axis labels.

```Python
# import plotly
import plotly.express as px

# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input, styled", labels={"value": "Medal Count", "variable": "Medal", "nation": "Olympic Nation"}, color_discrete_map={"gold": "gold", "silver": "silver", "bronze": "#c96"}, template="simple_white")

# update figure layout
fig.update_layout(font_family="Rockwell", showlegend=False)

# show figure
fig.show()
```

In the styled modified example, we again modified the field labels by passing a dictionary to `labels`.

We specified color by field value using `color_discrete_map`.

We set a style template using `template`.

We used `.update_layout()` to set a font family for the figure and axis titles, and also hid the legend.

We can also set the bar mode using `.update_layout()` with the `barmode` attribute. 

Setting `barmode` to `stack` produces a stacked bar chart.

### Grouped bar chart

Setting `barmode` to `group` produces a grouped bar chart.

### Horizontal bar chart

We can set the `orientation` attribute to `h` to produce a horizontal bar chart.
```Python
fig = px.bar(data, x="X field", y="Y field", orientation="h")
```

Remember in a horizontal bar chart, the `X` and `Y` axis values are the inverse of a vertical bar chart.

#### Additional resources

For more on bar charts in `plotly`:
- [`plotly`, Bar Charts in Python](https://plotly.com/python/bar-charts/)
- [`plotly`, Grouped Bar Chart](https://plotly.com/python/bar-charts/#grouped-bar-chart)
- [`plotly`, Stacked Bar Chart](https://plotly.com/python/bar-charts/#stacked-bar-chart)
- [`plotly`, Horizontal Bar Charts in Python](https://plotly.com/python/horizontal-bar-charts/)
- [`plotly.express.bar`](https://plotly.com/python-api-reference/generated/plotly.express.bar)
- [`plotly`, Python Figure Reference: `bar` Traces](https://plotly.com/python/reference/bar/)

### Pie Charts

We can create a pie chart using `px.pie()`.

An example using our global population sample data:
```Python
# import plotly
import plotly.express as px

# select dataframe subset
df = px.data.gapminder().query("year == 2007").query("continent == 'Europe'")

# filter dataframe to classify countries below a population size threshold as "Other countries"
df.loc[df['pop'] < 2.e6, 'country'] = 'Other countries' 

# create figure
fig = px.pie(df, values='pop', names='country', title='Population of European continent')

# show figure
fig.show()
```

Perhaps a useful example of the limited utility of pie charts.

In this example, we pass the filtered dataframe to `px.pie()`, and specify the `pop` field as the slice value and `country` as the slice name.

Another example using the restaurant bill and tip data.

```Python
# import plotly
import plotly.express as px

# load dataframe
df = px.data.tips()

# create figure
fig = px.pie(df, values='tip', names='day')

# show figure
fig.show()
```
In this example, we pass the entire data frame to `px.pie()` and assign `tip` as the slice value and `day` as the slice name.

Each day is a slice of the pie, and `plotly.express` and the `px.pie()` function have done the underlying calculations to show the aggregate tip data as a percent.

#### Donut Chart

A donut chart is a modified pie chart with an empty circle at the middle of the pie.

We can create a donut chart by creating a graph object and specifying a value for the `hole` parameter.

This example does not use `plotly.express` and instead creates the graph object manually.
```Python
# import plotly
import plotly.graph_objects as go

# set slice labels
labels = ['Oxygen','Hydrogen','Carbon_Dioxide','Nitrogen']

# set slice values
values = [4500, 2500, 1053, 500]

# create figure
fig = go.Figure(data=[go.Pie(labels=labels, values=values, hole=.3)])

# show figure
fig.show()
```

There's a lot to get into in terms of the differences between `plotly.express` function syntax and `plotly.graph_object` syntax.

For our purposes, we can focus on how values, labels, and a hole parameter are passed to `go.Figure()` and `go.Pie()` to create the plot.

#### Sunburst Charts

Multilevel pie charts are known as sunburst charts.

We can create a sunburst chart using the `plotly.express` `px.sunburst()` function.

Let's say we have a family tree that we want to represent using a sunburst chart.

With `px.sunburst()`, each row of the `DataFrame` is a sector of the sunburst (analogous to a slice of the pie in a pie chart).

```Python
# import plotly
import plotly.express as px

# create dictionary with data
data = dict(
    character=["Eve", "Cain", "Seth", "Enos", "Noam", "Abel", "Awan", "Enoch", "Azura"],
    parent=["", "Eve", "Eve", "Seth", "Seth", "Eve", "Eve", "Awan", "Eve" ],
    value=[10, 14, 12, 10, 2, 6, 6, 4, 4])

# create figure
fig =px.sunburst(
    data,
    names='character',
    parents='parent',
    values='value',
)

# show figure
fig.show()
```

A more complex example for the Kennedy family tree:

```Python
# import plotly
import plotly.express as px

# create dictionary with data
data = dict(
    person=["Patrick Joseph Kennedy", "John F. Fitzgerald", "Joseph P. Kennedy", "Rose Fitzgerald Kennedy", "Ted Kennedy", "John F. Kennedy", "Robert F. Kennedy", "Jean Kennedy", "Eunice Kennedy Shriver", "Patrick Joseph Kennedy II", "Caroline Kennedy", "Mark Kennedy Shriver", "Robert Shriver", "Maria Shriver", "Kathleen Kennedy", "Joseph Patrick Kennedy II", "Mary Kennedy", "Joseph Patrick Kennedy III"],
    parent=["", "", "Patrick Joseph Kennedy", "John Fitzgerald Kennedy", "Joseph P. Kennedy", "Joseph P. Kennedy", "Joseph P. Kennedy", "Joseph P. Kennedy", "Joseph P. Kennedy", "Ted Kennedy", "John F. Kennedy", "Eunice Kennedy Shriver", "Eunice Kennedy Shriver", "Eunice Kennedy Shriver", "Robert F. Kennedy", "Robert F. Kennedy", "Robert F. Kennedy", "Joseph Patrick Kennedy II"],
    value=[17, 17, 15, 15, 2, 2, 3, 1, 3, 1, 1, 1, 1, 1, 1, 2, 1, 1])

# create figure
fig =px.sunburst(
    data,
    names='person',
    parents='parent',
    values='value',
)

# show figure
fig.show()
```
#### Additional resources

For more on pie charts in `plotly`:
- [`plotly`, Pie Charts in Python](https://plotly.com/python/pie-charts/)
- [`plotly.express.pie`](https://plotly.com/python-api-reference/generated/plotly.express.pie)
- [`plotly`, Python Figure Reference: `pie` Traces](https://plotly.com/python/reference/pie/)

For more on sunburst charts in `plotly`:
- [`plotly`, Sunburst Charts in Python](https://plotly.com/python/sunburst-charts/)
- [`plotly.express.sunburst`](https://plotly.com/python-api-reference/generated/plotly.express.sunburst)
- [`plotly`, Python Figure Reference: `sunburst` Traces](https://plotly.com/python/reference/sunburst/)

### Bubble Charts

A bubble chart is as scatter plot in which the marker size is tied to a third dimension of the data.

We can create bubble charts in `plotly.express` using the `px.scatter()` function nad assigning the `size` parameter to a data field.

An example using a single year of the global population data, where per capita GDP is the `X` axis value, and average life expectancy is the `Y` axis value.

Marker marker size is determined by population.

```Python
# import plotly
import plotly.express as px

# create dataframe
df = px.data.gapminder()

# create figure
fig = px.scatter(df.query("year==2007"), x="gdpPercap", y="lifeExp", size="pop", color="continent", hover_name="country", log_x=True, size_max=60)

# show figure
fig.show()
```

In this example, we use `px.scatter()` to create a scatter plot.

By setting `size` to `pop`, the marker size is determined by the numeric value in the `pop` field. 

We also set a maximum marker size using `size_max`.

By setting `color` to `continent`, the marker color is determined by the `continent` field string.

We set a name or title for the hover labels using `hover_name`.

Setting `log_x` to `True` (the default for this attribute is `False`) means the `X` axis will be log-scaled in cartesian coordinates.

### Additional resources

For more on bubble charts in `plotly`:
- [`plotly`, Bubble Charts in Python](https://plotly.com/python/bubble-charts/)
- [`plotly.express.scatter`](https://plotly.com/python-api-reference/generated/plotly.express.scatter)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)

### Plotting Categorical Data

For our purposes, categorical data is defined as qualitative, nominal, or ordinal data that is discrete, or non-continuous.

Categorical data contrasts with numerical data that is continuous.

The axis type determines how the data is plotted in the resulting figure.

Axis types recognized in `plotly`:
- `linear` 
- `log`
- `date`
- `category`
- `multicategory`

The axis type is auto-detected by `plotly` based on the data linked to the specific axis.

If `plotly` does not recognize the data as `multicategory`, `date`, or `category` (it checks sequentially in that order), it defaults to `linear`.

When testing for `multicategory` data, `plotly` looks for to see if there is a nested array.

When testing for `date` or `category`, `plotly` requires more than twice as many distinct date or category strings as distinct numbers in order to choose one of these axis types.

We can imagine scenarios in which we are working with categorical data that would not be accurately auto-detected by `plotly`.

We can instruct `plotly` to recongize an axis as having categorical data through the `xaxis_type` and `yaxis_type` attributes.

An example of categorical data represented as a bar chart.
```Python
# import plotly
import plotly.express as px

# create figure
fig = px.bar(x=["a", "a", "b", 3], y = [1,2,3,4])

# update x axis type
fig.update_xaxes(type='category')

# show figure
fig.show()
```
In this example, the auto-detected `X` axis type would be `linear`.

By using `.update_xaxes(type='category')`, we force the `X` axis to be categorical.

We can also control the category order by passing a dictionary to the `category_orders` parameter.

An example with side-by-side bar charts of categorical data for the resturaunt and tip data.
```Python
# import plotly
import plotly.express as px

# load data
df = px.data.tips()

# create figure
fig = px.bar(df, x="day", y="total_bill", color="smoker", barmode="group", facet_col="sex",
             category_orders={"day": ["Thur", "Fri", "Sat", "Sun"],
                              "smoker": ["Yes", "No"],
                              "sex": ["Male", "Female"]})
# show figure
fig.show()
```

In addition to setting `color`, `barmode`, and `facet_col` parameters, we pass a dictionary to `category_orders` to determine the order for each category in the plot.

We can also automatically sort categories by name or total value by using `.update_xaxes()` or `.update_yaxes()` in combination with the `categoryorder` parameter.

Setting `categoryorder` to `category ascending` or `category descending` sorts categories alphabetically.

Setting `categoryorder` to `total ascending` or `total descending` sorts categories numerically by total value.

#### Additional resources

For more on categorical data and `plotly`:
- [`plotly`, Categorical Axes in Python](https://plotly.com/python/categorical-axes/)
- [`plotly`, Axes in Python](https://plotly.com/python/axes/)
- [`plotly`, Python Figure Reference: `layout.xaxis`](https://plotly.com/python/reference/layout/xaxis/)

### Maps

Up to this point, we have been working with data plotted on a 2D cartesian coordinate system, with `x` and `y` axes.

For our purposes, it's most useful to think of maps in the same way--as data plotted on a coordinate system.

Except for maps, that coordinate system is typically some type of latitude or longitude based projection, and the data to be plotted includes explicit location information (rather than a numerical or categorical field that can be mapped to an axis).

`plotly` supports two different types of maps.

***Mapbox maps*** are tile-based maps that are rendered using tiles that join together to form the map plot. 

***Geo maps*** are outline-based maps that are rendered using the `layout.geo` object  that contains map configuration information.

We'll start by looking at Geo outline-based maps before exploring Mapbox tile-based maps.

#### Geo maps

##### Base map layer

`plotly` Geo maps have a built-in base map layer composed of "physical" and "cultural" data from the [Natural Earth Dataset](https://www.naturalearthdata.com/downloads/).

We can show or hide, as well as modify, various components of this base layer.

We can take a look at the built-in base map, showing only country sub-units.
```Python
# import plotly
import plotly.graph_objects as go

# create figure
fig = go.Figure(go.Scattergeo())

# update figure to not show physical attributes and show country attributes
fig.update_geos(
    visible=False, resolution=50,
    showcountries=True, countrycolor="RebeccaPurple"
)

# update figure layout
fig.update_layout(height=300, margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

There are a few options for zooming or focusing the area represented in the base map.

We can set the `layout.geo.fitbounds` attribute to `locations` to automatically center the visual base map  range based on the data being plotted.
```Python
# import plotly
import plotly.express as px

# create geographic line plot
fig = px.line_geo(lat=[0,15,20,35], lon=[5,10,25,30])

# update figure to center and zoom base map based on data parameters
fig.update_geos(fitbounds="locations")

# udpate figure size and layout
fig.update_layout(height=300, margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

We can also set the scope of a map using a named sub-set.

Available named scopes include:
- `world`
- `usa`
- `europe`
- `asia`
- `africa`
- `north america`
- `south america`

Sorry, penguins and polar bears.

##### Point data

Now that we have a base map layer that will serve as the coordinate system for our plot, we can plot data using this coorinate system.

When we understand maps a just another time of plot that uses a different projection system, maps with markers are just another kind of scatterplot.

We can use the `px.scatter_geo()` function to plot point data with geospatial dimensions.

We can create a point map for the global population dataset.

```Python
# import plotly
import plotly.express as px

# load single year of data
df = px.data.gapminder().query("year == 2007")

# create figure
fig = px.scatter_geo(df, locations="iso_alpha", size="pop")

# show figure
fig.show()
```

In this exapmle, we pass the entire data frame `df` to the `px.scatter_geo()` function.

We use `locations` to note the column with location information.

The `size` parameter determines the size of each marker based on the `pop` field value.

Let's say we wanted to use a different type of global projection, and color the points by continent.

```Python
# import plotly
import plotly.express as px

# load single year of data
df = px.data.gapminder().query("year == 2007")

# create figure
fig = px.scatter_geo(df, locations="iso_alpha", size="pop", color="continent", hover_name="country", projection="natural earth")

# show figure
fig.show()
```

In the modified example, we set `color` to assign a color to each unique value in `continent`.

We set the `hover_name` to `country`.

And we set `projection` to `natural earth` to change the underlying base map layer.

We can also create a map from geospatial data stored in a `pandas` `DataFrame` using `GeoPandas`.

An example using US airport traffic data.

```Python
# import plotly
import plotly.graph_objects as go

# import pandas
import pandas as pd

# load data
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2011_february_us_airport_traffic.csv')

# set column names and data types
df['text'] = df['airport'] + '' + df['city'] + ', ' + df['state'] + '' + 'Arrivals: ' + df['cnt'].astype(str)

# create figure
fig = go.Figure(data=go.Scattergeo(
        lon = df['long'],
        lat = df['lat'],
        text = df['text'],
        mode = 'markers',
        marker_color = df['cnt'],
        ))

# update figure layout with title and scope
fig.update_layout(
        title = 'Most trafficked US airports<br>(Hover for airport names)',
        geo_scope='usa',
    )

# show figure
fig.show()
```
In this example, we use `plotly`'s `graph_object` syntax to create the figure and specify which columns in the `dataframe` include latitude and longitude information.

##### Polygon data

We can easily imagine a scenario in which a map with point data (or a scatterplot on a map projection system) is not the most effective way to represent data.

For example, when working with geospatial units that are not singular latitude and longitude points, representing an area using a polygon may yield a more insightful plot.

When working with data at the county, state, country, etc. level, polygons may be preferable to points.

We call these kinds of maps ***choropleth maps***.

We can use the `px.choropleth()` function to create an outline-based choropleth map in `plotly`.

Choropleth maps require two main types of input to generate a map:
- ***Geometry information***: can be supplied using a GeoJSON file in which each feature (polygon) has an id field that can be used to connect attribute data; 
  * `plotly` includes built-in geometries for US states and world countries
- ***Attribute data***, or a list of values indexed by feature identifiers (an id reflected in the geometry information)

Let's take a quick look at the underlying JSON object for a sample GeoJSON file.

```Python
# import urlrequest
from urllib.request import urlopen

# import json package
import json

# load url data
with urlopen('https://raw.githubusercontent.com/plotly/datasets/master/geojson-counties-fips.json') as response:
    counties = json.load(response)

# select first feature in dataset
counties["features"][0]
```

We are now seeing the underlying JSON object for the first feature in the county GeoJSON data.
```JSON
{'type': 'Feature',
 'properties': {'GEO_ID': '0500000US01001',
  'STATE': '01',
  'COUNTY': '001',
  'NAME': 'Autauga',
  'LSAD': 'County',
  'CENSUSAREA': 594.436},
 'geometry': {'type': 'Polygon',
  'coordinates': [[[-86.496774, 32.344437],
    [-86.717897, 32.402814],
    [-86.814912, 32.340803],
    [-86.890581, 32.502974],
    [-86.917595, 32.664169],
    [-86.71339, 32.661732],
    [-86.714219, 32.705694],
    [-86.413116, 32.707386],
    [-86.411172, 32.409937],
    [-86.496774, 32.344437]]]},
 'id': '01001'}
 ```
 
 We have our geometric information loaded.
 
 Now on to the attribute data, or data values indexed by an id field.
 
 This example uses county-level unemployment data, indexed by [FIPS code](https://en.wikipedia.org/wiki/FIPS_county_code) as the unique id.
 
 ```Python
# import pandas
import pandas as pd

# load dataframe
df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/fips-unemp-16.csv",
                   dtype={"fips": str})
# show first five rows
df.head()
```

Now we can work with the geometric information and the attribute data to generate a choropleth map.

We do this using the `px.choropleth()` function.

```Python
# import urllib module
from urllib.request import urlopen

# import json module
import json

# load geometric data
with urlopen('https://raw.githubusercontent.com/plotly/datasets/master/geojson-counties-fips.json') as response:
    counties = json.load(response)

# import pandas
import pandas as pd

# load dataframe
df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/fips-unemp-16.csv",
                   dtype={"fips": str})

# import plotly
import plotly.express as px

# create figure
fig = px.choropleth(df, geojson=counties, locations='fips', color='unemp',
                           color_continuous_scale="Viridis",
                           range_color=(0, 12),
                           scope="usa",
                           labels={'unemp':'unemployment rate'}
                          )

# update figure margins
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

Behold, a choropleth map showing unemployment rates for US counties.

In this example, we set the `counties` GeoJSON as the geometric data.

We specify the common field to use to connect the two datasets, `fips`.

We base polygon color on the `unemp` field using `color`.

We set the number of colors or color range using `range_color`.

We select a continuous colormap using `color_continuous_scale`.

And we update the `unemp` field name using `labels`.

##### Additional resources

For more on outline-based maps in `plotly`:
- [`plotly`, Map Configuration and Styling in Python](https://plotly.com/python/map-configuration/)
- [`plotly`, Scatter Plots on Maps in Python](https://plotly.com/python/scatter-plots-on-maps/)
- [`plotly`, Choropleth Maps in Python](https://plotly.com/python/choropleth-maps/)
- [`plotly`, Plotly Python Open Source Graphing Library Maps](https://plotly.com/python/maps/)

For more on `GeoPandas`: [https://geopandas.org](https://geopandas.org/)

#### Mapbox and tile maps

Now on to tile-based maps.

***Mapbox maps*** are tile-based maps that are rendered using tiles that join together to form the map plot. 

Mapbox tile maps are layer-based.

The base map layer is defined by `layout.mapbox.style`.

The data layer plotted on the base map is controlled by a `plotly.express` or `graph_object` function.

`layout.mapbox.layers` can define additional layers as needed.

In the default `plotly` settings, these layers are rendered in the following order:
- base layer (`layout.mapbox.style`)
- data layer (`trace` object)
- additional layers (`layout.mapbox.layers`)

In these examples, Mapbox refers to the open-source Mapbox GL JavaScript library.

The Mapbox JavaScript library is integrated into `plotly`.

Some components of Mapbox are available without an access token.

Other Mapbox components require an access token to use.

Navigate to https://docs.mapbox.com/help/how-mapbox-works/access-tokens/ to set up a free Mapbox account and obtain an access token.

When needed, the token can be set using the `px.set_mapbox_access_token()` configuration function.

##### Base map layer

There are a few options for base map layers using `layout.mapbox.style`.

`white-bg` is an empty white canvas and includes no external HTTP requests.

Raster tiles from public tile servers:
- `open-street-map
- `carto-positron`
- `carto-darkmatter`
- `stamen-terrain`
- `stamen-toner`
- `stamen-watercolor`

Vector tiles from Mapbox service (require access token):
- `basic`
- `streets`
- `outdoors`
- `light`
- `dark`
- `satellite`
- `satellite-streets`

We can also specify the base map layer using a Mapbox service style URL.

These styles require an access token. 

Browse the [Mapbox Galery](https://www.mapbox.com/gallery/).

Let's create a base map layer using `open-street-map`.

```Python
# import plotly
import plotly.express as px

# create figure
fig = px.scatter_mapbox(height=300)

# update figure base map layer
fig.update_layout(mapbox_style="open-street-map")

# update figure margin
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

We could change the value assigned to `mapbox_style` to change the base map layer style.

In a situation where we are loading  a base map layer from a URL, we would set `mapbox_style` to `white-bg` to create a blank canvas for the external base map layer style.

Another example that uses public tiles from the United States Geological Survey (USGS). No access token required.

```Python
# import plotly
import plotly.express as px

# create figure
fig = px.scatter_mapbox()

# update figure base map
fig.update_layout(
    mapbox_style="white-bg",
    mapbox_layers=[
        {
            "below": 'traces',
            "sourcetype": "raster",
            "sourceattribution": "United States Geological Survey",
            "source": [
                "https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer/tile/{z}/{y}/{x}"
            ]
        }
      ])

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

One last example using `dark` from the Mapbox service. An access token is required.

```Python
# load mapbox access token
token = open(".mapbox_token").read()

# import plotly
import plotly.express as px

# create figure
fig = px.scatter_mapbox()

# update figure base map layer
fig.update_layout(mapbox_style="dark", mapbox_accesstoken=token)

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

##### Point data

Now we can use the `px.scatter_mapbox()` function to add point data to our figure.

This example take sthe `open-street-map` base map from the previous section and adds point data for 1,000 US cities with highest population count.

```Python
# import pandas
import pandas as pd

# load dataframe
us_cities = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/us-cities-top-1k.csv")

# import plotly 
import plotly.express as px

# create figure
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_discrete_sequence=["fuchsia"], zoom=3, height=300)

# update figure base map
fig.update_layout(mapbox_style="open-street-map")

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

We specify which fields in the `us_cities` dataframe incldue latitude and longitude information (`lat` and `lon`).

We set a color sequence with discrete colors.

But since no field is assigned for a color attribute, all points are the same color.

If we wanted to color the points based on population size, we would want to switch to a continuous color scale.
```Python
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_continuous_scale=px.colors.sequential.Viridis, color="Population", zoom=3, height=300)
```

If we wanted out point size to be based on the population value, we would modify the `size` parameter.
```Python
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_discrete_sequence=["fuchsia"], zoom=3, height=300, size="Population")
```

Another example that uses rideshare data for Montreal.

In this example, point size is based on the number of car hours (`car_hours`) and point color is based on time of day (`peak_hour`).

```Python
# import plotly
import plotly.express as px

# set mapbox access token
px.set_mapbox_access_token(open(".mapbox_token").read())

# load data
df = px.data.carshare()

# create figure
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours", color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10)
# show figure
fig.show()
```

We pass the entire dataframe to `px.scatter_mapbox` and specify which fields include geospatial information.

We set `color` and `size` and assign a maximum size for the points.

`plotly` includes a number of built-in discrete and continuous colormaps.

To learn more about the built-in colormap options:
- [`plotly`, Continuous Color Scales and Color Bars in Python](https://plotly.com/python/colorscales/#color-scales-in-plotly-express)
- [`plotly`, Built-In Continuous Color Scales in Python](https://plotly.com/python/builtin-colorscales/#using-builtin-continuous-color-scales)
- [`plotly`, Discrete Colors in Python](https://plotly.com/python/discrete-color/)

We can also use `px.scatter_mapbox()` in combination with `GeoPandas`.

An example that includes point data for natural earth cities.
```Python
# import plotly
import plotly.express as px

# import geopandas
import geopandas as gpd

# load data
geo_df = gpd.read_file(gpd.datasets.get_path('naturalearth_cities'))

# set mapbox access token
px.set_mapbox_access_token(open(".mapbox_token").read())

# create figure
fig = px.scatter_mapbox(geo_df,
                        lat=geo_df.geometry.y,
                        lon=geo_df.geometry.x,
                        hover_name="name",
                        zoom=1)
# show figure
fig.show()
```

##### Polygon data

We can also create tile-map choropleth maps using the `px.choropleth_mapbox()` function.

Tile-map choropleth maps require the same two main types of input to generate a map:
- ***Geometry information***: can be supplied using a GeoJSON file in which each feature (polygon) has an id field that can be used to connect attribute data; 
  * `plotly` includes built-in geometries for US states and world countries
- ***Attribute data***, or a list of values indexed by feature identifiers (an id reflected in the geometry information)

We'll use the same county unemployment data from the previous choropleth map section.

With `px.choropleth_mapbox()`, each row of the dataframe is represented by a polygon.

An sample choropleth map of the county unemployment data, using the base layer `carto-positron` which does not require an access token.

```Python
# import urllib
from urllib.request import urlopen

# import json
import json

# load geojson data
with urlopen('https://raw.githubusercontent.com/plotly/datasets/master/geojson-counties-fips.json') as response:
    counties = json.load(response)

# import pandas
import pandas as pd

# load attribute data as dataframe
df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/fips-unemp-16.csv",
                   dtype={"fips": str})

# import plotly
import plotly.express as px

# create figure
fig = px.choropleth_mapbox(df, geojson=counties, locations='fips', color='unemp',
                           color_continuous_scale="Viridis",
                           range_color=(0, 12),
                           mapbox_style="carto-positron",
                           zoom=3, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'unemp':'unemployment rate'}
                          )

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

And again, we have a choropleth map showing unemployment rates for US counties.

In this example, we set the `counties` GeoJSON as the geometric data.

We specify the common field to use to connect the two datasets, `fips`.

We base polygon color on the `unemp` field using `color`.

We set the number of colors or color range using `range_color`.

We select a continuous colormap using `color_continuous_scale`.

And we update the `unemp` field name using `labels`.

##### Additional resources

For more on tile-based maps in `plotly`:
- [`plotly`, Map Configuration and Styling in Python](https://plotly.com/python/map-configuration/)
- [`plotly`, Mapbox Map Layers in Python](https://plotly.com/python/mapbox-layers/)
- [`plotly`, Scatter Plots on Mapbox in Python](https://plotly.com/python/scattermapbox/)
- [`plotly`, Mapbox Choropleth Maps in Python](https://plotly.com/python/mapbox-county-choropleth/)
- [`plotly`, Plotly Python Open Source Graphing Library Maps](https://plotly.com/python/maps/)

For more on `GeoPandas`: [https://geopandas.org](https://geopandas.org/)

### Tables

`plotly.express` does not include a table function, but we can create a graph object table using `go.Figure()` in combination with `go.Table()`.

We can create two columns of data with sample scores for `A` and `B` letter grades.

```Python
# import plotly
import plotly.graph_objects as go

# create figure with data
fig = go.Figure(data=[go.Table(header=dict(values=['A Scores', 'B Scores']),
                 cells=dict(values=[[100, 90, 80, 90], [95, 85, 75, 95]]))
                     ])
# show figure
fig.show()
```

There's a lot to get into in terms of the differences between `plotly.express` function syntax and `plotly.graph_object` syntax.

For our purposes, we can focus on how the table header takes a dictionary with column labels, and the cells also take a dictionary with two lists of values.

These dictionaries are passed to `go.Figure()` and `go.Table()` to create the plot.

We could also generate a table from data stored in a `pandas` `DataFrame`.

This example also includes style parameters for the table.
```Python
# import plotly
import plotly.graph_objects as go

# import pandas
import pandas as pd

# create dataframe
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/2014_usa_states.csv')

# create figure
fig = go.Figure(data=[go.Table(
    header=dict(values=list(df.columns),
                fill_color='paleturquoise',
                align='left'),
    cells=dict(values=[df.Rank, df.State, df.Postal, df.Population],
               fill_color='lavender',
               align='left'))
])

# show figure
fig.show()
```

This example includes style attributes like `fill_color` and `align` for both `header` and `cells`.

For `header`, this example takes a dictionary with the `DataFrame` column labels as a list, and the `DataFrame` column values as values for the `cells`.

### Additional resources

For more on tables in `plotly`:
- [`plotly`, Tables in Python](https://plotly.com/python/table/)
- [`plotly`, Python Figure Reference: `table` Traces](https://plotly.com/python/reference/table/)

### Additional Chart Types and Resources

Dot plots:
- [`plotly`, Dot Plots in Python](https://plotly.com/python/dot-plots/)

Gantt charts:
- [`plotly`, Gantt Charts in Python](https://plotly.com/python/gantt/)
- [`plotly.figure_factory.create_gantt`](https://plotly.com/python-api-reference/generated/plotly.figure_factory.create_gantt.html)

Filled area plots:
- [`plotly`, Filled Area Plots in Python](https://plotly.com/python/filled-area-plots/)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter)
  * [`line` parameter](https://plotly.com/python/reference/scatter/#scatter-line)
  * [`fill` parameter](https://plotly.com/python/reference/scatter/#scatter-fill)
  
Sankey Diagram:
- [`plotly`, Sankey Diagram in Python](https://plotly.com/python/sankey-diagram/)
- [`plotly`, Python Figure Reference: `sankey` Traces](https://plotly.com/python/reference/sankey)

Treemap charts:
- [`plotly`, Treemap Charts in Python](https://plotly.com/python/treemaps/)
- [`plotly.express.treemap`](https://plotly.com/python-api-reference/generated/plotly.express.treemap)
- [`plotly`, Python Figure Reference: `treemap` Traces](https://plotly.com/python/reference/treemap)

For more types of statistical charts: [`plotly`, Plotly Python Open Source Graphing Library Statistical Charts](https://plotly.com/python/statistical-charts/)

For more types of scientific charts: [`plotly`, Plotly Python Open Source Graphing Library Scientific Charts](https://plotly.com/python/scientific-charts/)

For more types of financial charts: [`plotly`, Plotly Python Open Source Graphing Library Financial Charts](https://plotly.com/python/financial-charts/)

For more types of maps: [`plotly`, Plotly Open Source Graphing Library Maps](https://plotly.com/python/maps/)

Full gallery of chart types: [`plotly`, Plotly Python Open Source Graphing Library](https://plotly.com/python/)


## Exporting from `plotly`

At this point, we have generated a *wide* range of interactive plots using `plotly`.

Now what?

`plotly` figures are interactive when viewed in a web browser.

But since version 4.0, `plotly` is offline only, which means all figures are rendered in the local environment.

Even if figures are displaying in a web browser window, the figure does not exist online--the web browser is loading a figure from the local environment.

For more on `plotly`'s move to offline-only: plotly, ["Plotly.py 4.0 is here: Offline Only, Express First, Displayable Anywhere"](https://medium.com/plotly/plotly-py-4-0-is-here-offline-only-express-first-displayable-anywhere-fc444e5659ee) *Medium* (22 July 2019).

### Static image export

We can export `plotly` figures as static image file formats (`.png`, `.jpeg`, `.svg`, and `.pdf`).

Static image generation requires the [`Kaleido` package](https://github.com/plotly/Kaleido).

To install `Kaleido`:
- using `pip`: `pip install kaleido`
- using `conda`: `conda install conda-forge python-kaleido`

Once a figure has been created, we can use the `.write_image()` method in combination with `plotly` to write the figure to an image file.

```Python
# write to png
fig.write_image("filepath/filename.png")

# write to jpeg
fig.write_image("filepath/filename.jpeg")

# write to svg
fig.write_image("filepath/filename.svg")

# write to pdf
fig.write_image("filepath/filename.pdf")
```

For more on static image export: [`plotly`, Static Image Export in Python](https://plotly.com/python/static-image-export/)

### Saving to HTML 

We can also export `plotly` figures as `HTML` files which will can be loaded in a web browser.

Unlike static image exports, these `HTML` files will include the interactivity of the `plotly` figure.

Once a figure has been created, we can use the `.write_html()` method to save the figure as an `HTML` file.

```Python
fig.write_html("filepath/filename.html")
```

For more on HTML file export: [`plotly`, Interactive HTML Export in Python](https://plotly.com/python/interactive-html-export/)

### `dash`

We may want to create an interactive web application featuring a `plotly` figure.

We see this kind of interactivity in dashboard-style interfaces:
SUCH AS

We can use the `dash` web application framework in combination with `plotly` to "publish" a figure as an interactive web application.

`dash` was developed by the Plotly team and released in 2017.

In addition to a limited free open-source version, Plotly also offers paid enterprise versions of `dash`.

What exactly is `dash`?

"Dash is a productive Python framework for building web analytic applications. Written on top of Flask, Plotly.js, and React.js, Dash is ideal for building data visualization apps with highly custom user interfaces in pure Python. It's particularly suited for anyone who works with data in Python. Through a couple of simple patterns, Dash abstracts away all of the technologies and protocols that are required to build an interactive web-based application. Dash is simple enough that you can bind a user interface around your Python code in an afternoon. Dash apps are rendered in the web browser. You can deploy your apps to servers and then share them through URLs. Since Dash apps are viewed in the web browser, Dash is inherently cross-platform and mobile ready" (`plotly`, [Introduction to Dash](https://dash.plotly.com/introduction)).

For those familiar with RStudio's [Shiny package](v) (designed to build interactive web applications from within the R/RStudio programming environment), `dash` was originally pitched as the equivalent package for Python.

Though originally built exclusively for `Python`, `dash` has since released versions for R/RStudio and Julia.

For more background on `dash`:
- plotly, ["Introducing Dash"](https://medium.com/plotly/introducing-dash-5ecf7191b503) *Medium* (21 June 2017)
- Plotly, ["PLOTCON 2016: Chris Parmer, Dash: Shiny for Python"](https://youtu.be/5BAthiN0htc) *YouTube* (1 December 2016)
- `plotly`, [Dash Enterprise App Gallery](https://dash-gallery.plotly.host/Portal/)
- [Plotly, Dash GitHub repository](https://github.com/plotly/dash)

To install `dash`:
- using `pip`: `pip install dash`
- in Jupyter notebook using `pip`: `pip install jupyter-dash`
- in Jupyter notebook using `conda`: `conda install -c conda-forge -c plotly jupyter-dash`

The remainder of this tutorial focuses on `dash` outside the Jupyter notebook environment.

For more on using `dash` in a notebook environment: plotly, [Jupyter-Dash Github Repository](https://github.com/plotly/jupyter-dash)

#### Basic `dash` syntax

`dash` apps include two main components.

The app ***layout*** describes what the application looks like.

The app ***interactivity*** describes the application's interactivity.

`dash` uses pre-built Python classes for all visual components of the application (which can be customized if needed using JavaScript and React.js).

The basic syntax for creating an application using `dash`:

```Python
# at this point the figure has already been created and updated/configured/customized as needed

# import dash components
import dash
import dash_core_components as dcc
import dash_html_components as html

# create app
app = dash.Dash()

# set app layout
app.layout = html.Div([
    dcc.Graph(figure=fig)
])

# run app
app.run_server(debug=True, use_reloader=False)
```

Let's create an app using our tile-based choropleth map.
```Python
# import urllib
from urllib.request import urlopen

# import json
import json

# load geojson data
with urlopen('https://raw.githubusercontent.com/plotly/datasets/master/geojson-counties-fips.json') as response:
    counties = json.load(response)

# import pandas
import pandas as pd

# load attribute data as dataframe
df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/fips-unemp-16.csv",
                   dtype={"fips": str})

# import plotly
import plotly.express as px

# create figure
fig = px.choropleth_mapbox(df, geojson=counties, locations='fips', color='unemp',
                           color_continuous_scale="Viridis",
                           range_color=(0, 12),
                           mapbox_style="carto-positron",
                           zoom=3, center = {"lat": 37.0902, "lon": -95.7129},
                           opacity=0.5,
                           labels={'unemp':'unemployment rate'}
                          )

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()

# import dash components
import dash
import dash_core_components as dcc
import dash_html_components as html

# create app
app = dash.Dash()

# set app layout
app.layout = html.Div([
    dcc.Graph(figure=fig)
])

# run app
app.run_server(debug=True, use_reloader=False)
```

At the bottom of each documentation page for a `plotly` figure type will be a "What About Dash?" section that provides a brief overview of how to publish that figure in a `dash` application.

For example, [link to the "What About Dash?"](https://plotly.com/python/scattermapbox/#what-about-dash) section of the "Scatter Plots on Mapbox in Python" page.

#### Customizing `dash` layout with `dash-html-components`

This example makes very few modifications to `app.layout`.

We can start to customize a `dash` app by using an external style sheet.

Similar to how we use CSS in combination with HTML, external style sheets can also be loaded and applied in `dash`.
```Python
# load style sheet; this example uses URL; could also use local .css file
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

# call style sheet when starting app
app = dash.Dash(APP_NAME, external_stylesheets=external_stylesheets)
```

We can also start to modify components of the application by declaring HTML tags.

Remember in HTML, tags like `<h1>`, `<p>`, etc. are used for styling and formatting.

The `dash_html_components` library has a component for every HTML tag.

We can create declarations for those elements to govern how they are formatted or styled in the `dash` application.

This is similar to how we create declarations in an external style sheet.

Let's modify our app layout to include a `H1` title, a `div` subtitle, and a `Graph` object.

```Python
# omitted code creates and customizes figure

# import dash components
import dash
import dash_core_components as dcc
import dash_html_components as html

# load style sheet; this example uses URL; could also use local .css file
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

# call style sheet when starting app
app = dash.Dash(Test_App, external_stylesheets=external_stylesheets)

# set app layout
app.layout = html.Div(children=[
    html.H1(children='Hello Dash'),

    html.Div(children='''
        Dash: A web application framework for Python.
    '''),

    dcc.Graph(
        id='example-graph',
        figure=fig
    )
])

# run app
app.run_server(debug=True, use_reloader=False)
```

We see the component declarations nested under `app.layout`.

`dash` generates an HTML element for each of these components.

For example, `dash` takes `html.H1(children='Hello Dash')` and generates `<h1>Hello Dash</h1>`.

`dash` can also take keyword arguments as part of these component declarations.

Let's say we want to override the external style sheet or set formatting for an element not convered in the style sheet.
```Python
# import dash components
import dash
import dash_core_components as dcc
import dash_html_components as html

# load style sheet; this example uses URL; could also use local .css file
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

# call style sheet when starting app
app = dash.Dash(Test_App, external_stylesheets=external_stylesheets)

# color declaration 
colors = {'background': '#111111', 'text': '#7FDBFF'}

# omitted code creates figure

# update figure layout using colors dictionary keys
fig.update_layout(plot_bgcolor=colors['background'], paper_bgcolor=colors['background'], font_color=colors['text'])

# set app layout
app.layout = html.Div(style={'backgroundColor': colors['background']}, children=[
    html.H1(
        children='Hello Dash',
        style={
            'textAlign': 'center',
            'color': colors['text']
        }
    ),

    html.Div(children='Dash: A web application framework for Python.', style={
        'textAlign': 'center',
        'color': colors['text']
    }),

    dcc.Graph(
        id='example-graph-2',
        figure=fig
    )
])

# run app
if Test_App == '__main__':
    app.run_server(debug=True)
```

We create the `colors` dictionary with `background` and `text` keys and color values.

We apply those custom colors to the figure using `fig.update_layout`.

We apply those custom colors as keyword arguments for the `app.layout` components.

For more on the `dash-html-components` library: [`plotly`, Dash HTML Components](https://dash.plotly.com/dash-html-components)

For more on the `dash` layout options: [`plotly`, Dash Layout](https://dash.plotly.com/layout)

#### Customizing `dash` using `dash-core-components`

Where `dash` really shines (and has functionality that compares with RStudio Shiny) is in the higher-level core components.

These core components include things like:
- Dropdown input menu
- Slider
- Range slider
- Input box
- Input text area
- Checkboxes
- Radio buttons
- Buttons
- Single date picker
- Date range picker
- File upload
- Multi-tab disply

These core components are generated through a combination of JavaScript, HTML, and CSS in combination with the React.js library.

The syntax for `dash-core-components` is similar to the HTML element declarations in the previous sections.

A few examples are provided below.

##### Dropdown

```Python
# import dash core components
import dash_core_components as dcc

# sample code for a dropdown menu
dcc.Dropdown(
    options=[
        {'label': 'New York City', 'value': 'NYC'},
        {'label': 'Montréal', 'value': 'MTL'},
        {'label': 'San Francisco', 'value': 'SF'}
    ],
    value='MTL'
)

# this example takes a list of dictionaries as the label and value pairs for the dropdown; value sets the default dropdown valu

# sample code for multi-select dropdown
dcc.Dropdown(
    options=[
        {'label': 'New York City', 'value': 'NYC'},
        {'label': 'Montréal', 'value': 'MTL'},
        {'label': 'San Francisco', 'value': 'SF'}
    ],
    multi=True,
    value="MTL"
) 

# setting multi to True allows for multi-select

# for more on dropdown components: https://dash.plotly.com/dash-core-components/dropdown
```
##### Slider

```Python
# import dash core components
import dash_core_components as dcc

# sample code for a slider
dcc.Slider(
    min=-5,
    max=10,
    step=0.5,
    value=-3
)  

# this example sets the min and max value for the slider, as well as the step increments and default value

# another example that includes slider labels
dcc.Slider(
    min=0,
    max=9,
    marks={i: 'Label {}'.format(i) for i in range(10)},
    value=5,
)

# this example sets marks for each slider value

# for more on slider components: https://dash.plotly.com/dash-core-components/slider
```
##### RangeSlider

```Python
# import dash core components
import dash_core_components as dcc

# sample code for a range slider
dcc.RangeSlider(
    count=1,
    min=-5,
    max=10,
    step=0.5,
    value=[-3, 7]
)  

# example specifies min and max values, default positions, and step increment

# another range slider example with labels
dcc.RangeSlider(
    marks={i: 'Label {}'.format(i) for i in range(-5, 7)},
    min=-5,
    max=6,
    value=[-3, 4]
)

# again marks is used to set the mark position and label text

# for more on range sliders: https://dash.plotly.com/dash-core-components/rangeslider
```

##### Input

```Python
# import dash core components
import dash_core_components as dcc

# sample code for an input box
dcc.Input(
    placeholder='Enter a value...',
    type='text',
    value=''
)  

# placeholder sets the placeholder text; type sets the input type; value sets the default value

# for more on input: https://dash.plotly.com/dash-core-components/input
```

##### TextArea

```Python
# import dash core components
import dash_core_components as dcc

# sample code for a text area box
dcc.Textarea(
    placeholder='Enter a value...',
    value='This is a TextArea component',
    style={'width': '100%'}
)

# placeholder sets the placeholder value, value sets the default value, and style sets the box width

# for more on Textarea: https://dash.plotly.com/dash-core-components/textarea 
```

##### Checkboxes

```Python
# import dash core components
import dash_core_components as dcc

# sample code for vertical list of checkboxes (default includes multi-select)
dcc.Checklist(
    options=[
        {'label': 'New York City', 'value': 'NYC'},
        {'label': 'Montréal', 'value': 'MTL'},
        {'label': 'San Francisco', 'value': 'SF'}
    ],
    value=['MTL', 'SF']
)  

# options set the label and value for each check box, and value sets the default values

# another example with a horizontal or inline list of checkboxes
dcc.Checklist(
    options=[
        {'label': 'New York City', 'value': 'NYC'},
        {'label': 'Montréal', 'value': 'MTL'},
        {'label': 'San Francisco', 'value': 'SF'}
    ],
    value=['MTL', 'SF'],
    labelStyle={'display': 'inline-block'}
)

# modifying labelStyle changes the layout

# for more on Checklist: https://dash.plotly.com/dash-core-components/checklist
```

##### Other core component types

You're starting to get the picture.

For more examples and documentation:
- [`dcc.RadioItems()`](https://dash.plotly.com/dash-core-components/radioitems)
- [`html.Button()`](https://dash.plotly.com/dash-html-components/button)
- [`dcc.DatePickerSingle()`](https://dash.plotly.com/dash-core-components/datepickersingle)
- [`dcc.DatePickerRange()`](https://dash.plotly.com/dash-core-components/datepickerrange)
- [`dcc.Upload()`](https://dash.plotly.com/dash-core-components/upload)
- [`dcc.Tabs()`](https://dash.plotly.com/dash-core-components/tabs)
- [`dcc.Graph()`](https://dash.plotly.com/dash-core-components/graph)


For more on the `dash_core_components` library: [`plotly`, Dash Core Components](https://dash.plotly.com/dash-core-components)

For more on the `dash_html_components` library: [`plotly`, Dash HTML Components](https://dash.plotly.com/dash-html-components)

#### Setting up callbacks

At this point, these layout components are interactive in the sense that you can interact with them.

But the components are not response, in the sense that interacting with them does not change the app's behavior.

We need to make the layout components responsive and interactive.

We can do this in `dash` using callback functions.

In `dash` syntax, callback functions are Python functions called by `dash` whenever an input component's property changes.

An example that uses a responsive input box.
```Python
# import dash components
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output

# set external style sheet
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

# initialize app
app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

# configure app layout
app.layout = html.Div([
    html.H6("Change the value in the text box to see callbacks in action!"),
    html.Div(["Input: ",
              dcc.Input(id='my-input', value='initial value', type='text')]),
    html.Br(),
    html.Div(id='my-output'),

])

# decorator that tells dash to call named function when input value changes so output components reflect that change
@app.callback(
    Output(component_id='my-output', component_property='children'),
    Input(component_id='my-input', component_property='value')
)

# name output function
def update_output_div(input_value):
    return 'Output: {}'.format(input_value)


# initialize app
if __name__ == '__main__':
    app.run_server(debug=True)
```

Let's walk through what happens in this example.

The application inputs and outputs are described using the `@app.callback` decorator, similar to the layout and component declarations covered previously.

The decorator instructs `dash` to call this function whenever the input value changes, so the output components are updated accordingly.

What you name the function arguments is up to you, as long as the names in the function definition match the names in the callback.

The `@app.callback` decorator references components described in `app.layout`.

Thus the component names in `@app.callback` need to reflect the component names used with `app.layout`.

In this example, those component names are `my-input` and `my-output`.

We see those names set using the `id` parameter with `app.layout`, and reflected in the callback.

The `@app.callback` decorator should always come immediately before the `def` function definition.

For more on function decorators in Python: [`python`, PEP 318 -- Decorators for Functions and Methods](https://www.python.org/dev/peps/pep-0318/)

In `dash` syntax, application inputs and outputs are treated as component properties. 

In this example, the `my-input` component is set to take the input as its `value`, and `my-output` is set to reflect the `my-input` value.

Whenever an input property changes (in this example characters in the input box change), the callback function is automatically called.

`dash` provides the function with the new input value and updates the output component property.

Note that we had to import `from dash.dependencies import Input, Output`, which is different than `dash_core_components.Input`.

Taken together, this functionality is called ***reactive programming***.

The keyword arguments used to describe each component become incredibly important when setting up callback functions.

Let's look at another application that uses callbacks.

In this examle, global population data is plotted as a bubble chart.

Points are colored by continent, sized by population, and a slider is used to mark each year of available data.

```Python
# import dash components and plotly
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import plotly.express as px

# import pandas
import pandas as pd

# load dataframe
df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/gapminderDataFiveYear.csv')

# load external stylesheet
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

# initialize app
app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

# set app layout with graph and slider components
app.layout = html.Div([
    dcc.Graph(id='graph-with-slider'),
    dcc.Slider(
        id='year-slider',
        min=df['year'].min(),
        max=df['year'].max(),
        value=df['year'].min(),
        marks={str(year): str(year) for year in df['year'].unique()},
        step=None
    )
])


# set callback for slider and graph; note the slider is the input and the graph is the output
@app.callback(
    Output('graph-with-slider', 'figure'),
    Input('year-slider', 'value'))

# function definition for slider
def update_figure(selected_year):
    filtered_df = df[df.year == selected_year]

    fig = px.scatter(filtered_df, x="gdpPercap", y="lifeExp",
                     size="pop", color="continent", hover_name="country",
                     log_x=True, size_max=55)

    fig.update_layout(transition_duration=500)

    return fig


# launch application
if __name__ == '__main__':
    app.run_server(debug=True)
```

This example loads as `pandas` dataframe using `pd.read_csv()`.

Loading the data outside of the callback functions means that the data loading operation is only done once, rather than each time the function is called.

The callback does not modify the original data--it works with `pandas` filters to to create copies of the `dataframe`.

NOTE: callback functions should NEVER alter the underlying `dataframe`.

We also set the layout transition time using `fig.update_layout()` in combination with `transition_duration`. 

This parameter gives the resulting figure smooth transitions between slider year values.

For more on `dash` callbacks:
- [`plotly`, Basic Dash Callbacks](https://dash.plotly.com/basic-callbacks)
- [`plotly`, Advanced Callbacks](https://dash.plotly.com/advanced-callbacks)

#### Additional resources

We're just scratching the surface of what you can do using `dash`.

Callback functions can include multiple inputs and outputs, as well as chained callback functions.
- [`plotly`, Basic Callbacks](https://dash.plotly.com/basic-callbacks)

`dash` also allows for interactive visualizations that change based on how the user is interacting with the visualization.
- [`plotly`, Interactive Visualizations](https://dash.plotly.com/interactive-graphing)

To learn more, consult the [Dash User Guide](https://dash.plotly.com/).

The [Dash Enterprise App Gallery](https://dash-gallery.plotly.host/Portal/) includes sample apps with the back-end `dash` code.

See also: Daniel Barker, ["A short Python tutorial using the open-source Plotly "Dash" library"](https://towardsdatascience.com/a-short-python-tutorial-using-the-open-source-plotly-dash-library-part-i-e59fb1f1a457) *Towards Data Science* (24 April 2018).

In these examples, we are still working in your local environment.

The `dash` app may run in a web browser, but it uses your computer as a local host (`localhost`).

For a `dash` app to be available via the World Wide Web, you need to deploy it to a server.

A few free server options that support public Flask applications (the framework `dash` is built on) include Heroku and Reclaim Hosting.

*Alternatively you could take Prof. Walden's "Minimal Computing" class and build your own LAMP stack server.*

More information on deplying a `dash` app using Heroku (free): [`plotly`, Heroku for Sharing Public Dash apps for Free](https://dash.plotly.com/deployment).

See also: Elsa Scola, ["The Easiest Way to Deploy Your Dash App for Free"](https://towardsdatascience.com/the-easiest-way-to-deploy-your-dash-app-for-free-f92c575bb69e) *Towards Data Science* (2 May 2020).

Another option for acquiring a domain and web hosting is Reclaim Hosting.

"Founded in 2013, Reclaim Hosting provides educators and institutions with an easy way to offer their students domains and web hosting that they own and control. Our goal is to make the process of offering a flexible web space and domain name to your students as easy as possible and giving you the support you need to make it all happen" ([About Reclaim Hosting](https://reclaimhosting.com/about/)).

At the time this tutorial was written (December 2020), [Reclaim Hosting's personal plan](https://reclaimhosting.com/shared-hosting/) is $30 annually and includes 2 GB of storage.

For more information in deploying a Flask app using Reclaim Hosting (or another cPanel provider):
- [`python`, Flask: Deploy an App](https://python-adv-web-apps.readthedocs.io/en/latest/flask_deploy.html)
- Tony Hirst, ["Creating a Simple Python Flash App via cPanel on Reclaim Hosting"](https://blog.ouseful.info/2016/09/17/creating-a-simple-python-flask-app-running-on-reclaim-hosting/) *OUseful.Info* (17 September 2016)

# Practice problems

There are no practice problems. There is only final project proposal work.

# Lab Notebook Questions

