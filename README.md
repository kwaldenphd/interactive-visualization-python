# Lab #12: Visualizing Data Using Matplotlib

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.


## Lab Goals

## Acknowledgements

https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html 

https://pandas.pydata.org/docs/user_guide/visualization.html

https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html

# Table of Contents

# `pandas` and `matplotlib`

Having to load data manually to build a visualization or plot gets cumbersome quickly.

In many situations, we might want to work with data in a `pandas` `DataFrame` when building a visualization.

`pandas` includes a `.plot()` attribute that interacts with the `matplotlib` API to generate plots.

The `pandas` `.plot()` attribute relies on the `matplotlib` API to generate plots, so our work with `matplotlib` will come in handy when we need to customize plots generated using `.plot()`.

And in many cases, the `.plot()` syntax is similar to `matplotlib` `OO` syntax.

## Plotting in `pandas` using `.plot()`

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


# Enter, `plotly`!

# Practice problems

# Lab Notebook Questions

# Lab Notebook Questions
