# Interactive Visualization in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab provides an overview of interactive data visualization in Python using `plotly`. It provides an overview and comparison of the `bokeh` and `plotly` packages. It provides an overview of `plotly` functionality, focusing on `plotly.express` functions for a variety of plot types, including 2D cartesian coordinate system plots and mapping using geospatial data. It ends with an overview of export options for `plotly` figures.

By the end of this lab, students will be able to:
- Understand the basic components of interactive Python visualization packages `bokeh` and `pandas`
- Understand the basic syntax used to generate a `plotly` figure for a variety of plot types, using `plotly.express` functions
- Understand the syntax and options available for customizing a `plotly` figure
- Understand the export options for a `plotly` figure
- Be able to use `plotly.express` functions to generate their own figures, with a basic level of customization
- Understand how to navigate and interact with `plotly` documentation for tutorials and troubleshooting

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=95dd1702-5640-4af4-811f-ae3e017f8091">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements

The author consulted the following resources when writing  this tutorial:
- [`plotly` documentation and tutorials](https://plotly.com/python/)

# Table of Contents

- [Lecture & Live Coding](#lecture--live-coding)
- [Lab notebook template](#lab-notebook-template)
- [Setup and environment](#setup-and-environment)
- [Overview](#overview)
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
    * [Tables](#tables)
  * [Plotting Categorical Data](#plotting-categorical-data)
  * [Lab Notebook Question 1](#lab-notebook-question-1)
- [Maps](#maps)
  * [Geo Maps, or Outline-Based Maps](#geo-maps-or-outline-based-maps)
  * [Mapbox and Tile-Based Maps](#mapbox-and-tile-based-maps)
  * [Lab Notebook Question 2](#lab-notebook-question-2)
- [Additional Plot Types and Resources](#additional-plot-types-and-resources)
- [Exporting from `plotly`](#exporting-from-plotly)
  * [Static Image Export](#static-image-export)
  * [Saving to HTML](#saving-to-html)
  * [`dash`](#dash)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here to access the lab procedure as a Jupyter Notebook](https://drive.google.com/file/d/1gEz2spZgoGbPVUqsDRovR8UqUpiZsv-8/view?usp=sharing)

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=95dd1702-5640-4af4-811f-ae3e017f8091">Lecture/live coding playlist</a></td>
  </tr>
  </table>

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=853b474f-bf54-432f-8982-ae3d0036773e">Overview</a></td>
  </tr>
  </table>

# Lab Notebook Template

[Link to access the lab notebook template (Jupyter Notebook)](https://drive.google.com/file/d/1J4UZ0HBBSQYzTjbzAelzfwgSZ-YIdKeN/view?usp=sharing)

# Setup and Environment

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=853b474f-bf54-432f-8982-ae3d0036773e">Overview</a></td>
  </tr>
  </table>

## Plotly

This lab explores two packages used for interactive visualization in Python: `bokeh` and `plotly`.

To install `bokeh`:
- using `pip`: `pip install bokeh`
- using `conda`: `conda install -c bokeh`


To install `plotly`:
- using `pip`: `pip install plotly`
- using `conda`: `conda install -c plotly`

## GeoPandas

Later in this lab, we'll be using a package called `GeoPandas` for plotting spatial data.

Installing and configuring `Geopandas` requires creating a new Python environment.

A few resources that can get folks started:
 
**Installing and Configuring `geopandas`**:
- Anaconda
  * Tanish Gupta, "[Fastest Way to Install Geopandas in Jupyter Notebooks](https://medium.com/analytics-vidhya/fastest-way-to-install-geopandas-in-jupyter-notebook-on-windows-8f734e11fa2b)" *Analytics Vidhya* (6 December 2020)
  * Anaconda, "[conda-forge packages, geopandas](https://anaconda.org/conda-forge/geopandas)" *Anaconda documentation*
  * GeoPandas, "[Installation](https://geopandas.org/getting_started/install.html)" *GeoPandas documentation*
- Google CoLab
  * Abdishakur Hassan, Jupyter notebook on using `geopandas` in Google CoLab, from "[Geographic data science tutorials with Python](https://github.com/shakasom/GDS)" *GitHub repository*
    * [Google CoLab](https://colab.research.google.com/github/shakasom/GDS/blob/master/Part1%20-%20Introduction.ipynb)
    * [GitHub](https://github.com/shakasom/GDS/blob/master/Part1%20-%20Introduction.ipynb)

Additional `GeoPandas` resources:
- Jonathan Soma, "[Mapping with geopandas](https://jonathansoma.com/lede/foundations-2017/classes/geopandas/mapping-with-geopandas/)" from 2017 "[Foundations of Computing](https://jonathansoma.com/lede/foundations-2017/)" course, Columbia Graduate School of Journalism
- CoderzColumn, "[Plotting Static Maps with geopandas](https://coderzcolumn.com/tutorials/data-science/plotting-static-maps-with-geopandas-working-with-geospatial-data)" *CoderzColumn* (11 March 2020)
- GeoPandas, "[Plotting with Geoplot and GeoPandas](https://geopandas.org/gallery/plotting_with_geoplot.html)" *GeoPandas documentation*

## Mapbox Access Token

Later in this lab, we'll be working with features of the Mapbox API that require an access token.

Sign up for a free Mapbox account:
- https://account.mapbox.com/auth/signup/

Once you have signed up and logged in, click `Token` in the top level menu (between `Dashboard` and `Statistics`).
- https://account.mapbox.com/access-tokens/

Click the `Create a token` button to create a new access token:
- https://account.mapbox.com/access-tokens/create

Choose a descriptive name for your token ("Elements of Computing Lab" works fine). The default settings for which boxes are checked/unchecked are fine.

Click the `Create token` button at the bottom of the page.

Save this token value (string of numbers and letters) for later in the lab.

## Geocoding Data

Lab notebook question 2 asks you to generate map visualizations.

There are a number of sample datasets used in the lab that have geospatial attributes.

But if you're wanting to work with your own data and it does not have geospatial attributes (latitude and longitude), you'll need to add that information via a process called geocoding.

Free online geocoding services:
- [LocalFocus data journalism batch geocoder](https://geocode.localfocus.nl/)
- [Texas A&M Geocoding Services](https://geoservices.tamu.edu/Services/Geocode/)
  * *Requires creating a free account*
 
There are also Python libraries that support geocoding.
- [`GeoPy`](https://geopy.readthedocs.io/en/stable/)
- [`Geocoder`](https://geocoder.readthedocs.io/providers/Mapbox.html) (requires a free Mapbox API key)
- Abdishakur, ["Geocode with Python"](https://towardsdatascience.com/geocode-with-python-161ec1e62b89) *Towards Data Science* (15 September 2019)

# Overview

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ec1f17b7-a517-4dc1-a65c-ae3d003b9730">Bokeh and Plotly Background</a></td>
  </tr>
  </table>

Up to this point, we have been generic static image plots in Python using a combination of `pandas`, `matplotlib`, and `seaborn`. But in many cases we may want to generate interactive plots that can exist on the web.

We see this type of interactivity in data journalism projects:
- *NewYorkTimes* [TheUpshot](https://www.nytimes.com/section/upshot)
- [*FiveThirtyEight*](https://fivethirtyeight.com/)
- [*The Guardian*](https://www.theguardian.com/data)
- *The Atlantic*, ["The Language of The State of the Union"](https://www.theatlantic.com/politics/archive/2015/01/the-language-of-the-state-of-the-union/384575/) (18 January 2015)

We also see this kind of interactivity in dashboard-style interfaces, like the [Johns Hopkins University COVID-19 Dashboard](https://coronavirus.jhu.edu/map.html).

The two leading Python packages that can be used to generate interactive visualizations for the web are `bokeh` and `plotly`. We'll go over a brief overview for each, with some comparison considerations, before focusing on `plotly`.

## `bokeh`

"Bokeh is an interactive visualization library for modern web browsers. It provides elegant, concise construction of versatile graphics, and affords high-performance interactivity over large or streaming datasets. Bokeh can help anyone who would like to quickly and easily make interactive plots, dashboards, and data applications" ([bokeh documentation](https://docs.bokeh.org/en/latest/index.html))

`bokeh` emerged in 2013, and uses a glyph and model based approach when building interactive visualizations. `bokeh` is built on `D3.js`, a JavaScript library for interactive visualization. Full customization in `bokeh` requires some knowledge of JavaScript.                                                                                                                                                 

Sample code and output for a `bokeh` plot.

```Python
# import bokeh
from bokeh.plotting import figure, output_file, show

# create figure
p = figure(plot_width = 400, plot_height = 400)

# add data to figure
p.circle([1, 2, 3, 4, 5], [6, 7, 2, 4, 5], size=15, line_color="navy", fill_color="orange", fill_alpha=0.5)

# show figure
show(p)
```
<p align="center"><a href="https://github.com/kwaldenphd/interactive-visualization-python/blob/main/Figure_1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/interactive-visualization-python/blob/main/Figure_1.png?raw=true" /></a></p>

For more on `bokeh`:
- [`bokeh` documentation](https://docs.bokeh.org/en/latest/index.html#)
- [`bokeh`, Installation](https://docs.bokeh.org/en/latest/docs/installation.html)
- [`bokeh`, User Guide](https://docs.bokeh.org/en/latest/docs/user_guide.html)
- [`bokeh`, Tutorial](htthttps://mybinder.org/v2/gh/bokeh/bokeh-notebooks/7b6da26945e284b19df07daecc6beabdb7adbe81)
- [`bokeh`, Reference](https://docs.bokeh.org/en/latest/docs/reference.html#refguide)
- Charlie Harper, "Visualizing Data with Bokeh and Pandas," *The Programming Historian* 7 (2018), [https://doi.org/10.46430/phen0081](https://doi.org/10.46430/phen0081)

## `plotly`

"Plotly is a technical computing company headquartered in Montreal, Quebec, that develops online data analytics and visualization tools. Plotly provides online graphing, analytics, and statistics tools for individuals and collaboration, as well as scientific graphing libraries for Python, R, MATLAB, Perl, Julia, Arduino, and REST" ([Wikipedia](https://en.wikipedia.org/wiki/Plotly)).

The `plotly` Python graphing library is supported by the Plotly company. Plotly relies on Python and the Django framework, using JavaScript, D3.js, HTML, and CSS for its front-end. Plotly files are stored on Amazon Web Services' Simple Storage Service (S3). The company was founded in 2012 and went on to be a featured startup at 2013 PyCon, sponsoring the SciPy conference in 2018. During Series A funding, Plotly raised $5.5 million, supported by MHS Capital, Siemens Venture Capital, Rho Ventures, Real Ventures, and Silicon Valley Bank.

Plotly offers a range of products, some of which are free or open-source, and others that are subscription based.
- ***Dash***: an open-source web application framework for Python, R, and Julia
- ***Chart Studio***: a graphical user interface for analyzing and visualizing data; single-user version is free, enterprise deployments have a pricing model
- ***API libraries***: open-source graphing libraries for Python, R, and Julia
- ***Plotly Apps***: Google Chrome app
- ***PLotly.js***: open-source JavaScript graphic and dashboard library
- ***Plotly Enterprise***: pricing model for local Plotly installation and deployment

In recent years, Plotly has moved into machine learning and artificial intelligence app support and artificial intelligence supply chain technology and continues to expand its enterprise pricing options. 
- For more on Plotly history: [Plotly, "About Us"](https://plotly.com/about-us/)
- For more on Plotly products:
  - [Dash Enterprise](https://plotly.com/dash/)
  - [Consulting and Training](https://plotly.com/consulting-and-oem/)
  - [Chart Studio](https://plotly.com/chart-studio/)

Plotly's enterprise products are used by corporations that include NVIDIA, Tesla, Shell, Citi Bank, and Amgen. Plotly's Chart Studio product is used by a range of journalism outfits and companies, including S&P Global, The Washington Post, Wired, Tesla, and Medium.

## `bokeh` vs. `plotly`

At first glance, `bokeh` and `plotly` appear to have similar features and functionality. Both are based on JavaScript libraries, can work with data stored in `pandas`, and generate interactive web applications.

The packages have very different syntax for how they build visualizations and applications, and they rely on different back-end infrastructure when deploying web applications. In addition to having the support and infrastructure of the Plotly company, `plotly` has a significantly larger user community comprised of individuals and corporations. `plotly` graphing libraries are also available in languages other than Python, most notably R and Julia, while `bokeh` is designed for Python, with the stand-alone BokehJS library available for JavaScript.

This lab focuses on `plotly`, but the `bokeh` resources highlighted above are a useful place to start for working with the other package. For more in-depth `bokeh` and `plotly` comparisons:
- Paul Iacomi, ["Plotly vs. Bokeh: Interactive Python Visualisation Pros and Cons"](https://pauliacomi.com/2020/06/07/plotly-v-bokeh.html) *personal blog* (7 June 2020)
- stackshare, ["Bokeh vs Plotly](https://stackshare.io/stackups/bokeh-vs-plotly)
- Flavian, ["Bokeh vs Dash- Which is the Best Framework for Python?](https://www.sicara.ai/blog/2018-01-30-bokeh-dash-best-dashboard-framework-python) *Sicara* (20 February 2020)
- reddit, ["Plotly vs Bokeh vs..."](https://www.reddit.com/r/Python/comments/5nwk9r/plotly_vs_bokeh_vs/) (2017)
- Scott Fitzpatrick, ["Creating Python Dashboards: Dash Vs Bokeh"](https://www.activestate.com/blog/dash-vs-bokeh/) *Active State* (19 September 2019)
- Gabriela Moreira Mafra, ["Choosing one of many Python visualization tools"](https://blog.magrathealabs.com/choosing-one-of-many-python-visualization-tools-7eb36fa5855f) *Magrathea Lab Blog* (22 September 2018)
- Antoine Hue, ["Which library should I use for my Python dashboard?"](https://towardsdatascience.com/which-library-should-i-use-for-my-dashboard-c432726a52bf) *Towards Data Science* (31 August 2020)

# Getting Started with `plotly`

To install `plotly`:
- using `pip`: `pip install plotly`
- using `conda`: `conda install -c plotly`
- using Jupyter Notebook: `pip install "notebook>=5.3" "ipywidgets>=7.2"`
- using `conda` in Jupyter Notebook: `conda install "notebook>=5.3" "ipywidgets>=7.2"`

## The Mechanics of `plotly`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=9853137f-8a7a-428b-842c-ae3d003ec609">Plotly Mechanics</a></td>
  </tr>
  </table>

Plotly.js, the JavaScript library `plotly` is based on understands figures as trees with named nodes called attributes. The root node of the tree has three top-level attributes.

- The top-level ***`data`*** attribute consists of a list of dicts referred to as traces.
  - Each trace has a plot type (scatter, bar, pie, etc.), and is drawn on a single subplot. Traces can have a single legend, and other attributes depending on trace type.

- The top-level ***`layout`*** attribute is referred to as "the layout" and consists of a dict with attributes that control non-data parts of the figure. Parts of the figure governed by the `layout` attribute include:
  - Dimensions and margins
  - Templates, fonts, colors, hover labels
  - Titles and legends 
  - Non-data marks such as annotations, shapes, and images
  - Controls like buttons, toggles, menus, or sliders

- The top-level ***`frames`*** attribute does not exist for all types of plots. `frames` consists of a list of dicts that define sequential frames in an animated plot. Each frame in the sequence has its own `data` attribute (and other parameters).

When building a figure, you do not have to populate every attribute of every object. The JavaScript layer can compute default values for some unspecified attributes.

Let's look at an example for a simple line plot, using `plotly`:

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
```
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

A few notes on this figure structure:
- 2D Cartesian coordinate system subplots are the most commonly-used type of subplot. In `plotly`, traces compatible with these subplots support `xaxis` and `yaxis` attributes. Trace types compatible with 2D cartesian subplots include scatterplots, bar charts, histograms, and box plots.

- Both `X` and `Y` axes support a `type` attribute. The `type` attribute can modify a trace to show continuous values, temporal values, or categorical values.

Additional info:
- Figure data structure: [`plotly`, "The Figure Data Structure in Python"](https://plotly.com/python/figure-structure/)
- `plotly` fundamental syntax: [Plotly Python Open Source Graphing Library Fundamentals](https://plotly.com/python/plotly-fundamentals/)

## `plotly.express`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=7c15d7c1-c984-47fe-ab3c-ae3d004193bb">Plotly Express (Scatter Plots, Line Plots, Bar Charts)</a></td>
  </tr>
  </table>

The `plotly.express` module contains functions that can create entire figures at once. `plotly.express` functions are designed to be a user-friendly point of entry to the `plotly` package. A graph object is created as part of any `plotly.express` function, but the point of the `plotly.express` function is to significantly reduce the amount of code needed to create, customize, and render the graph object.

### Scatter Plots

To create a scatterplot using `plotly.express`, we use the `px.scatter()` function, which takes values for the `X` and `Y` axis. Without any additional arguments, the default formatting and style options are applied.

```Python
# create figure 
fig = px.scatter(x=[0, 1, 2, 3, 4], y=[0, 1, 4, 9, 16])

# show figure
fig.show()
```

Everything from tick marks to axis labels to grid lines to hover labels has been generated by the `plotly.express` defaults. To create a scatterplot from data stored in a `DataFrame`, the same general syntax specifying `X` and `Y` values still applies.

An example using data about flowers.
```Python
# load sample data already stored as a dataframe
df = px.data.iris()

# create figure
fig = px.scatter(df, x="sepal_width", y="sepal_length")

# show figure
fig.show()
```

In the `dataframe` example, we passed the entire data frame to `px.scatter()`, and specify columns to use for the `X` and `Y` axis. In the resulting figure, we can see how `plotly` assigns the column names as axis labels.

We can modify point color and size to reflect underlying values in the data frame (using `color` and `size`). We can also modify the information displayed in the hover label (using `hover_data`).

```Python
# load sample data already stored as a dataframe
df = px.data.iris()

# create figure
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species", size="petal_length", hover_data=["petal_width"])

# show figure
fig.show()
```

In this modified example, `color` specifies what field to use to color points, `size` specifies what field to use to size points, and `hover_data` adds fields not already incorporated in the figure to the hover label, which now includes 5 different fields.

For more on scatter plots in `plotly`:
- [`plotly`, Scatter Plots in Python](https://plotly.com/python/line-and-scatter/)
- [`plotly.express.scatter`](https://plotly.com/python-api-reference/generated/plotly.express.scatter)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)
- [`plotly`, Python Figure Reference: `scattergl` Traces](https://plotly.com/python/reference/scattergl/)

### Line Plots

We can create a simple line plot using `px.line()`. This example uses example data on life expectancy.

```Python
# load dataframe subset 
df = px.data.gapminder().query("country=='Canada'")

# create figure
fig = px.line(df, x="year", y="lifeExp", title='Life expectancy in Canada')

# show figure
fig.show()
```

In this example, we pass a subset of the `gapminder` dataframe to the `px.line()` function. We specify which fields to use for the `X` and `Y` axis values, and we give the figure a title.

Let's say we wanted to create a line plot with data for two countries. We could filter the data frame accordingly and use the `color` parameter.

```Python
# load dataframe subset 
df = px.data.gapminder().query("continent=='Oceania'")

# create figure
fig = px.line(df, x="year", y="lifeExp", color='country', title='Life Expectancy by Country')

# show figure
fig.show()
```

Let's say we want to modify the line plot to include a line for individual countries and color the lines by continent.

```Python
# load dataframe subset
df = px.data.gapminder().query("continent != 'Asia'")

# create figure
fig = px.line(df, x="year", y="lifeExp", color='continent', line_group='country', hover_name='country', title='Country Life Expectancy by Continent')

# show figure
fig.show()
```

In the modified example, we color the lines by continent and group the lines by country. We also use `line_group` to group rows in a column into lines and `hover_name` to set a title or name for the hover labels. The country name is now at the top of each hover label.

For more on line plots in `plotly`:
- [`plotly`, Line Charts in Python](https://plotly.com/python/line-charts/)
- [`plotly.express.line`](https://plotly.com/python-api-reference/generated/plotly.express.line)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)

### Bar Charts

We can create a bar chart using `px.bar()`. In the default settings, each row of the dataframe is represented as a rectangular mark.

An example using population data from the previous example's dataset.

```Python
# load subset of existing dataframe
data_canada = px.data.gapminder().query("country == 'Canada'")

# create figure
fig = px.bar(data_canada, x='year', y='pop')

# show figure
fig.show()
```

In this example, the `year` column is assigned as the `X` axis value, and the `pop` column is assigned as the `Y` axis value.

We can also generate a stacked bar chart using `px.bar()`. Let's take a look at a stacked bar chart for sample data stored in two different formats. As we learned in the `pandas` lab, data can be stored in a long or wide form.
- ***Long-form data*** has one row per observation and one column per variable. Also known as tidy data.
- ***Wide-form data*** has one row per value of the first variable, and one column per value of the second value.

A quick comparison of long and wide data for the same Olympic medal dataset.

```Python
# create data table from long dataframe
long_df = px.data.medals_long()

# show long data table
long_df
```

```Python
# create data table from long dataframe
wide_df = px.data.medals_wide()

# show long data table
wide_df
```

`plotly.express` and `px.bar()` can generate the same plot from either data form.

#### Stacked Bar Charts

To create a stacked bar chart using the long data form:
```Python
# load dataframe
long_df = px.data.medals_long()

# create figure
fig = px.bar(long_df, x="nation", y="count", color="medal", title="Long-Form Input")

# show figure
fig.show()
```

To create a stacked bar chart using the wide data form:
```Python
# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input")

# show figure
fig.show()
```

In the wide-format example, we pass a list of columns to the `Y` axis. For the wide-format example, we might want to relabel the fields when generating the hover labels.
```Python
# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input, relabelled", labels={"value": "count", "variable": "medal"})

# show figure
fig.show()
```

In the modified example, we passed a dictionary to `labels` to manually rename those fields in the hover label. If we wanted to change the styling for the wide-format example, we could specify a style template (similar to a style sheet), a colormap, and axis labels.

```Python
# load dataframe
wide_df = px.data.medals_wide()

# create figure
fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide-Form Input, styled", labels={"value": "Medal Count", "variable": "Medal", "nation": "Olympic Nation"}, color_discrete_map={"gold": "gold", "silver": "silver", "bronze": "#c96"}, template="simple_white")

# update figure layout
fig.update_layout(font_family="Rockwell", showlegend=False)

# show figure
fig.show()
```

In the styled modified example, we again modified the field labels by passing a dictionary to `labels`. A few other notes on this example:
- We specified color by field value using `color_discrete_map`.
- We set a style template using `template`.
- We used `.update_layout()` to set a font family for the figure and axis titles, and also hid the legend.

We can also set the bar mode using `.update_layout()` with the `barmode` attribute. Setting `barmode` to `stack` produces a stacked bar chart.

### Grouped Bar Charts

Setting `barmode` to `group` produces a grouped bar chart.

### Horizontal Bar Charts

We can set the `orientation` attribute to `h` to produce a horizontal bar chart.
```Python
# horizontal bar chart
fig = px.bar(data, x="X field", y="Y field", orientation="h")
```

Remember in a horizontal bar chart, the `X` and `Y` axis values are the inverse of a vertical bar chart.

For more on bar charts in `plotly`:
- [`plotly`, Bar Charts in Python](https://plotly.com/python/bar-charts/)
- [`plotly`, Grouped Bar Chart](https://plotly.com/python/bar-charts/#grouped-bar-chart)
- [`plotly`, Stacked Bar Chart](https://plotly.com/python/bar-charts/#stacked-bar-chart)
- [`plotly`, Horizontal Bar Charts in Python](https://plotly.com/python/horizontal-bar-charts/)
- [`plotly.express.bar`](https://plotly.com/python-api-reference/generated/plotly.express.bar)
- [`plotly`, Python Figure Reference: `bar` Traces](https://plotly.com/python/reference/bar/)

### Pie Charts

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=2941d6b5-b9bd-49a7-bc76-ae3d0048934a">Pie Charts</a></td>
  </tr>
  </table>

We can create a pie chart using `px.pie()`. An example using our global population sample data:
```Python
# select dataframe subset
df = px.data.gapminder().query("year == 2007").query("continent == 'Europe'")

# filter dataframe to classify countries below a population size threshold as "Other countries"
df.loc[df['pop'] < 2.e6, 'country'] = 'Other countries' 

# create figure
fig = px.pie(df, values='pop', names='country', title='Population of European continent')

# show figure
fig.show()
```

Perhaps a useful example of the limited utility of pie charts. In this example, we pass the filtered dataframe to `px.pie()`, and specify the `pop` field as the slice value and `country` as the slice name.

Another example using the restaurant bill and tip data.

```Python
# load dataframe
df = px.data.tips()

# create figure
fig = px.pie(df, values='tip', names='day')

# show figure
fig.show()
```

In this example, we pass the entire data frame to `px.pie()` and assign `tip` as the slice value and `day` as the slice name. Each day is a slice of the pie, and `plotly.express` and the `px.pie()` function have done the underlying calculations to show the aggregate tip data as a percent.

#### Donut Charts

A donut chart is a modified pie chart with an empty circle at the middle of the pie. We can create a donut chart by creating a graph object and specifying a value for the `hole` parameter. This example does not use `plotly.express` and instead creates the graph object manually.
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

There's a lot to get into in terms of the differences between `plotly.express` function syntax and `plotly.graph_object` syntax. For our purposes, we can focus on how values, labels, and a hole parameter are passed to `go.Figure()` and `go.Pie()` to create the plot.

#### Sunburst Charts

Multilevel pie charts are known as sunburst charts. We can create a sunburst chart using the `plotly.express` `px.sunburst()` function. Let's say we have a family tree that we want to represent using a sunburst chart. With `px.sunburst()`, each row of the `DataFrame` is a sector of the sunburst. Each sector in the sunburst chart is analogous to a slice of the pie in a pie chart.

```Python
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

For more on pie charts in `plotly`:
- [`plotly`, Pie Charts in Python](https://plotly.com/python/pie-charts/)
- [`plotly.express.pie`](https://plotly.com/python-api-reference/generated/plotly.express.pie)
- [`plotly`, Python Figure Reference: `pie` Traces](https://plotly.com/python/reference/pie/)

For more on sunburst charts in `plotly`:
- [`plotly`, Sunburst Charts in Python](https://plotly.com/python/sunburst-charts/)
- [`plotly.express.sunburst`](https://plotly.com/python-api-reference/generated/plotly.express.sunburst)
- [`plotly`, Python Figure Reference: `sunburst` Traces](https://plotly.com/python/reference/sunburst/)

### Bubble Charts

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ec4f1815-8c61-48dd-aaf3-ae3d004ad056">Bubble Charts</a></td>
  </tr>
  </table>

A bubble chart is a scatter plot in which the marker size is tied to a third dimension of the data. We can create bubble charts in `plotly.express` using the `px.scatter()` function and assigning the `size` parameter to a data field. An example using a single year of the global population data, where per capita GDP is the `X` axis value, and average life expectancy is the `Y` axis value. Marker marker size is determined by population.

```Python
# create dataframe
df = px.data.gapminder()

# create figure
fig = px.scatter(df.query("year==2007"), x="gdpPercap", y="lifeExp", size="pop", color="continent", hover_name="country", log_x=True, size_max=60)

# show figure
fig.show()
```

In this example, we use `px.scatter()` to create a scatter plot. By setting `size` to `pop`, the marker size is determined by the numeric value in the `pop` field. We also set a maximum marker size using `size_max`. By setting `color` to `continent`, the marker color is determined by the `continent` field string. We set a name or title for the hover labels using `hover_name`. Setting `log_x` to `True` (the default for this attribute is `False`) means the `X` axis will be log-scaled in cartesian coordinates.

For more on bubble charts in `plotly`:
- [`plotly`, Bubble Charts in Python](https://plotly.com/python/bubble-charts/)
- [`plotly.express.scatter`](https://plotly.com/python-api-reference/generated/plotly.express.scatter)
- [`plotly`, Python Figure Reference: `scatter` Traces](https://plotly.com/python/reference/scatter/)

### Tables

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ec4f1815-8c61-48dd-aaf3-ae3d004ad056">Tables</a></td>
  </tr>
  </table>

`plotly.express` does not include a table function, but we can create a graph object table using `go.Figure()` in combination with `go.Table()`. We can create two columns of data with sample scores for `A` and `B` letter grades.

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

There's a lot to get into in terms of the differences between `plotly.express` function syntax and `plotly.graph_object` syntax. For our purposes, we can focus on how the table header takes a dictionary with column labels, and the cells also take a dictionary with two lists of values. These dictionaries are passed to `go.Figure()` and `go.Table()` to create the plot. We could also generate a table from data stored in a `pandas` `DataFrame`.

This example also includes style parameters for the table.
```Python
# import plotly
import plotly.graph_objects as go

# import pandas
import pandas as pd

# create dataframe
df = pd.read_csv('https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/2014_usa_states.csv')

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

This example includes style attributes like `fill_color` and `align` for both `header` and `cells`. For `header`, this example takes a dictionary with the `DataFrame` column labels as a list, and the `DataFrame` column values as values for the `cells`.

For more on tables in `plotly`:
- [`plotly`, Tables in Python](https://plotly.com/python/table/)
- [`plotly`, Python Figure Reference: `table` Traces](https://plotly.com/python/reference/table/)

## Plotting Categorical Data

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c71f43c7-d9b9-4cdb-a645-ae3d004c615c">Categorical Data</a></td>
  </tr>
  </table>

For our purposes, categorical data is defined as qualitative, nominal, or ordinal data that is discrete, or non-continuous. Categorical data contrasts with numerical data that is continuous. The axis type determines how the data is plotted in the resulting figure.

Axis types recognized in `plotly`:
- `linear`
- `log`
- `date`
- `category`
- `multicategory`

The axis type is auto-detected by `plotly` based on the data linked to the specific axis.
- If `plotly` does not recognize the data as `multicategory`, `date`, or `category` (it checks sequentially in that order), it defaults to `linear`.
- When testing for `multicategory` data, `plotly` looks to see if there is a nested array.
- When testing for `date` or `category`, `plotly` requires more than twice as many distinct date or category strings as distinct numbers in order to choose one of these axis types.

We can imagine scenarios in which we are working with categorical data that would not be accurately auto-detected by `plotly`. We can instruct `plotly` to recognize an axis as having categorical data through the `xaxis_type` and `yaxis_type` attributes.

An example of categorical data represented as a bar chart.
```Python
# create figure
fig = px.bar(x=["a", "b", "c", "d"], y = [1,2,3,4])

# update x axis type
fig.update_xaxes(type='category')

# show figure
fig.show()
```

In this example, the auto-detected `X` axis type would be `linear`. By using `.update_xaxes(type='category')`, we force the `X` axis to be categorical.

We can also control the category order by passing a dictionary to the `category_orders` parameter. An example with side-by-side bar charts of categorical data for the restaurant and tip data.

```Python
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
- Setting `categoryorder` to `category ascending` or `category descending` sorts categories alphabetically.
- Setting `categoryorder` to `total ascending` or `total descending` sorts categories numerically by total value.

For more on categorical data and `plotly`:
- [`plotly`, Categorical Axes in Python](https://plotly.com/python/categorical-axes/)
- [`plotly`, Axes in Python](https://plotly.com/python/axes/)
- [`plotly`, Python Figure Reference: `layout.xaxis`](https://plotly.com/python/reference/layout/xaxis/)

## Lab Notebook Question 1

Q1: Build at least three different types of plots using plotly and data stored in a Pandas DataFrame. Include code + comments.
- *I encourage folks to use this question to explore visualizations you might use for the final project.*

Each plot should include the following elements:
- Title
- Axis labels
- Legend
- Scale or tickmarks
- Hover label
- Data source
 
Plot types to choose from:
- Line plots
- Bar chart
- Grouped bar chart
- Horizontal bar chart
- Stacked bar chart
- Histogram
- Box plot
- Area plot
- Scatter plot
- Pie chart
- Donut chart
- Sunburst chart
- Table

### Maps

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=59ec6f25-e51d-4e2b-9d2d-ae3d004f02a8">Mapping</a></td>
  </tr>
  </table>

Up to this point, we have been working with data plotted on a 2D cartesian coordinate system, with `x` and `y` axes. For our purposes, it's most useful to think of maps in the same way--as data plotted on a coordinate system. Except for maps, that coordinate system is typically some type of latitude or longitude based projection, and the data to be plotted includes explicit location information (rather than a numerical or categorical field that can be mapped to an axis).

A few resources related to geocoding:

Free online geocoding services:
- [LocalFocus data journalism batch geocoder](https://geocode.localfocus.nl/)
- [Texas A&M Geocoding Services](https://geoservices.tamu.edu/Services/Geocode/)
  * *Requires creating a free account*
 
There are also Python libraries that support geocoding.
- [`GeoPy`](https://geopy.readthedocs.io/en/stable/)
- [`Geocoder`](https://geocoder.readthedocs.io/providers/Mapbox.html) (requires a free Mapbox API key)
- Abdishakur, ["Geocode with Python"](https://towardsdatascience.com/geocode-with-python-161ec1e62b89) *Towards Data Science* (15 September 2019)

`plotly` supports two different types of maps.
- ***Mapbox maps*** are tile-based maps that are rendered using tiles that join together to form the map plot.
- ***Geo maps*** are outline-based maps that are rendered using the `layout.geo` object  that contains map configuration information.

### Geo Maps, or Outline-Based Maps

#### Base Map Layer

`plotly` Geo maps have a built-in base map layer composed of "physical" and "cultural" data from the [Natural Earth Dataset](https://www.naturalearthdata.com/downloads/). We can show or hide, as well as modify, various components of this base layer. For example, we can take a look at the built-in base map, showing only country sub-units.
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

There are a few options for zooming or focusing the area represented in the base map. We can set the `layout.geo.fitbounds` attribute to `locations` to automatically center the visual base map range based on the data being plotted.
```Python
# create geographic line plot
fig = px.line_geo(lat=[0,15,20,35], lon=[5,10,25,30])

# update figure to center and zoom base map based on data parameters
fig.update_geos(fitbounds="locations")

# udpate figure size and layout
fig.update_layout(height=300, margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

We can also set the scope of a map using a named sub-set. Available named scopes include:
- `world`
- `usa`
- `europe`
- `asia`
- `africa`
- `north america`
- `south america`
  * *Sorry, penguins and polar bears.*

#### Point Data

Now that we have a base map layer that will serve as the coordinate system for our plot, we can plot data using this coordinate system. When we understand maps are just another type of plot that uses a different projection system, maps with markers are just another kind of scatterplot. We can use the `px.scatter_geo()` function to plot point data with geospatial dimensions.

We can create a point map for the global population dataset.

```Python
# load single year of data
df = px.data.gapminder().query("year == 2007")

# create figure
fig = px.scatter_geo(df, locations="iso_alpha", size="pop")

# show figure
fig.show()
```

A few notes on this example:
- We pass the entire data frame `df` to the `px.scatter_geo()` function.
- We use `locations` to note the column with location information.
- The `size` parameter determines the size of each marker based on the `pop` field value.

Let's say we wanted to use a different type of global projection, and color the points by continent.

```Python
# load single year of data
df = px.data.gapminder().query("year == 2007")

# create figure
fig = px.scatter_geo(df, locations="iso_alpha", size="pop", color="continent", hover_name="country", projection="natural earth")

# show figure
fig.show()
```

A few notes on this modified example:
- We set `color` to assign a color to each unique value in `continent`.
- We set the `hover_name` to `country`.
- We set `projection` to `natural earth` to change the underlying base map layer.

We can also create a map from geospatial data stored in a `pandas` `DataFrame` using `GeoPandas`.
- [Link to more info on `GeoPandas` installation and configuration](#geopandas)

An example using US airport traffic data.

```Python
# import plotly
import plotly.graph_objects as go

# import pandas
import pandas as pd

# load data
df = pd.read_csv('https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/2011_february_us_airport_traffic.csv')

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

#### Polygon Data

We can easily imagine a scenario in which a map with point data (or a scatterplot on a map projection system) is not the most effective way to represent data. For example, when working with geospatial units that are not singular latitude and longitude points, representing an area using a polygon may yield a more insightful plot.

When working with data at the county, state, country, etc. level, polygons may be preferable to points. We call these kinds of maps ***choropleth maps***. We can use the `px.choropleth()` function to create an outline-based choropleth map in `plotly`.

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
with urlopen('https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/geojson-counties-fips.json') as response:
    counties = json.load(response)

# select first feature in dataset
counties["features"][0]
```

We are now seeing the underlying JSON object for the first feature in the county GeoJSON data.
```
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

We have our geometric information loaded. Now onto the attribute data, or data values indexed by an id field. This example uses county-level unemployment data, indexed by [FIPS code](https://en.wikipedia.org/wiki/FIPS_county_code) as the unique id.
 
 ```Python
# import pandas
import pandas as pd

# load dataframe
df = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/fips-unemp-16.csv",
                   dtype={"fips": str})
# show first five rows
df.head()
```

Now we can work with the geometric information and the attribute data to generate a choropleth map. We do this using the `px.choropleth()` function.

```Python
# import urllib module
from urllib.request import urlopen

# import json module
import json

# load geometric data
with urlopen('https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/geojson-counties-fips.json') as response:
    counties = json.load(response)

# import pandas
import pandas as pd

# load dataframe
df = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/fips-unemp-16.csv",
                   dtype={"fips": str})

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

Behold, a choropleth map showing unemployment rates for US counties. A few notes on this example:
- We set the `counties` GeoJSON as the geometric data
- We specify the common field to use to connect the two datasets, `fips`
- We base polygon color on the `unemp` field using `color`
- We set the number of colors or color range using `range_color`
- We select a continuous colormap using `color_continuous_scale`
- And we update the `unemp` field name using `labels`

For more on outline-based maps in `plotly`:
- [`plotly`, Map Configuration and Styling in Python](https://plotly.com/python/map-configuration/)
- [`plotly`, Scatter Plots on Maps in Python](https://plotly.com/python/scatter-plots-on-maps/)
- [`plotly`, Choropleth Maps in Python](https://plotly.com/python/choropleth-maps/)
- [`plotly`, Plotly Python Open Source Graphing Library Maps](https://plotly.com/python/maps/)

### Mapbox and Tile-Based Maps

Now on to tile-based maps. ***Mapbox maps*** are tile-based maps that are rendered using tiles that join together to form the map plot. Mapbox tile maps are layer-based, where the base map layer is defined by `layout.mapbox.style`. The data layer plotted on the base map is controlled by a `plotly.express` or `graph_object` function. `layout.mapbox.layers` can define additional layers as needed.

In the default `plotly` settings, these layers are rendered in the following order:
- base layer (`layout.mapbox.style`)
- data layer (`trace` object)
- additional layers (`layout.mapbox.layers`)

In these examples, Mapbox refers to the open-source Mapbox GL JavaScript library. The Mapbox JavaScript library is integrated into `plotly`. Some components of Mapbox are available without an access token. Other Mapbox components require an access token to use.

Navigate to https://docs.mapbox.com/help/how-mapbox-works/access-tokens/ to set up a free Mapbox account and obtain an access token. When needed, the token can be set using the `px.set_mapbox_access_token()` configuration function.

#### Base Map Layer

There are a few options for base map layers using `layout.mapbox.style`. `white-bg` is an empty white canvas and includes no external HTTP requests.

Raster tiles from public tile servers:
- `open-street-map`
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

We can also specify the base map layer using a Mapbox service style URL. These styles require an access token.

Let's create a base map layer using `open-street-map`.

```Python
# load dataframe
df = px.data.carshare()

# create plot
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours",
                  color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10,
                  mapbox_style="carto-positron")
# show figure
fig.show()
```

We could change the value assigned to `mapbox_style` to change the base map layer style. In a situation where we are loading  a base map layer from a URL, we would set `mapbox_style` to `white-bg` to create a blank canvas for the external base map layer style.

Another example that uses public tiles from the United States Geological Survey (USGS). No access token required.

```Python
# import packages
import pandas as pd

# load data
us_cities = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/us-cities-top-1k.csv")

# create figure
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_discrete_sequence=["fuchsia"], zoom=3, height=300)

# update figure layout
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

# update figure margin
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

One last example using `dark` from the Mapbox service. An access token is required.

```Python
# set mapbox access token
px.set_mapbox_access_token("YOUR ACCESS TOKEN GOES HERE")

# import plotly
import plotly.express as px

# load dataframe
df = px.data.carshare()

# create plot
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours",
                  color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10,
                  mapbox_style="dark")

# update figure layout
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})

# show figure
fig.show()
```

#### Point data

Now we can use the `px.scatter_mapbox()` function to add point data to our figure. This example takes the `open-street-map` base map from the previous section and adds point data for 1,000 US cities with the highest population count.

```Python
# import pandas
import pandas as pd

# load dataframe
us_cities = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/us-cities-top-1k.csv")

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

We specify which fields in the `us_cities` dataframe include latitude and longitude information (`lat` and `lon`). We set a color sequence with discrete colors. But since no field is assigned for a color attribute, all points are the same color.

If we wanted to color the points based on population size, we would want to switch to a continuous color scale.
```Python
# color points based on population value
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_continuous_scale=px.colors.sequential.Viridis, color="Population", zoom=3, height=300)
```

If we wanted our point size to be based on the population value, we would modify the `size` parameter.
```Python
# size points based on population value
fig = px.scatter_mapbox(us_cities, lat="lat", lon="lon", hover_name="City", hover_data=["State", "Population"],
                        color_discrete_sequence=["fuchsia"], zoom=3, height=300, size="Population")
```

Another example that uses rideshare data for Montreal. In this example, point size is based on the number of car hours (`car_hours`) and point color is based on time of day (`peak_hour`).

```Python
# set mapbox access token
px.set_mapbox_access_token("YOUR TOKEN GOES HERE")

# load data
df = px.data.carshare()

# create figure
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours", color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10)

# show figure
fig.show()
```

We pass the entire dataframe to `px.scatter_mapbox` and specify which fields include geospatial information. We set `color` and `size` and assign a maximum size for the points. 

`plotly` includes a number of built-in discrete and continuous colormaps. To learn more about the built-in colormap options:
- [`plotly`, Continuous Color Scales and Color Bars in Python](https://plotly.com/python/colorscales/#color-scales-in-plotly-express)
- [`plotly`, Built-In Continuous Color Scales in Python](https://plotly.com/python/builtin-colorscales/#using-builtin-continuous-color-scales)
- [`plotly`, Discrete Colors in Python](https://plotly.com/python/discrete-color/)

We can also use `px.scatter_mapbox()` in combination with `GeoPandas`. An example that includes point data for natural earth cities.
```Python
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

#### Polygon Data

We can also create tile-map choropleth maps using the `px.choropleth_mapbox()` function. Tile-map choropleth maps require the same two main types of input to generate a map:
- ***Geometry information***: can be supplied using a GeoJSON file in which each feature (polygon) has an id field that can be used to connect attribute data;
  * `plotly` includes built-in geometries for US states and world countries
- ***Attribute data***, or a list of values indexed by feature identifiers (an id reflected in the geometry information)

We'll use the same county unemployment data from the previous choropleth map section. With `px.choropleth_mapbox()`, each row of the dataframe is represented by a polygon. A sample choropleth map of the county unemployment data, using the base layer `carto-positron` which does not require an access token.

```Python
# import urllib
from urllib.request import urlopen

# import json
import json

# load geojson data
with urlopen('https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/geojson-counties-fips.json') as response:
    counties = json.load(response)

# import pandas
import pandas as pd

# load attribute data as dataframe
df = pd.read_csv("https://raw.githubusercontent.com/kwaldenphd/interactive-visualization-python/main/data/fips-unemp-16.csv",
                   dtype={"fips": str})

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

And again, we have a choropleth map showing unemployment rates for US counties. A few notes on this example:
- In this example, we set the `counties` GeoJSON as the geometric data.
- We specify the common field to use to connect the two datasets, `fips`.
- We base polygon color on the `unemp` field using `color`.
- We set the number of colors or color range using `range_color`.
- We select a continuous colormap using `color_continuous_scale`.
- And we update the `unemp` field name using `labels`.

For more on tile-based maps in `plotly`:
- [`plotly`, Map Configuration and Styling in Python](https://plotly.com/python/map-configuration/)
- [`plotly`, Mapbox Map Layers in Python](https://plotly.com/python/mapbox-layers/)
- [`plotly`, Scatter Plots on Mapbox in Python](https://plotly.com/python/scattermapbox/)
- [`plotly`, Mapbox Choropleth Maps in Python](https://plotly.com/python/mapbox-county-choropleth/)
- [`plotly`, Plotly Python Open Source Graphing Library Maps](https://plotly.com/python/maps/)

## Lab Notebook Question 2

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=7d148e6a-f514-409a-af42-ae3d005c3045">Lab Notebook Question 2</a></td>
  </tr>
  </table>

Q2: Build at least two different types of maps using plotly. Include code + comments.
- *I encourage folks to use this question to explore visualizations you might use for the final project.*

Each plot should include the following elements:
- Title
- Hover labels
- Scale
- Data source

Types of maps to choose from:
- Geo Maps, or Outline-Based Maps
  * Point map, `px.scatter_geo()`
  * Choropleth map `px.choropleth()`
- Mapbox or Tile-Based Maps
  * Point map, `px.scatter_mapbox()`
  * Choropleth map, `px.choropleth_mapbox()`

# Additional Plot Types and Resources

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

For more types of statistical charts:
- [`plotly`, Plotly Python Open Source Graphing Library Statistical Charts](https://plotly.com/python/statistical-charts/)

For more types of scientific charts:
- [`plotly`, Plotly Python Open Source Graphing Library Scientific Charts](https://plotly.com/python/scientific-charts/)

For more types of financial charts:
- [`plotly`, Plotly Python Open Source Graphing Library Financial Charts](https://plotly.com/python/financial-charts/)

For more types of maps:
- [`plotly`, Plotly Open Source Graphing Library Maps](https://plotly.com/python/maps/)

Full gallery of chart types:
- [`plotly`, Plotly Python Open Source Graphing Library](https://plotly.com/python/)

# Exporting from `plotly`

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=9b28d303-5222-411a-b8fc-ae3d005cf32f">Exporting From Plotly</a></td>
  </tr>
  </table>

`plotly` figures are interactive when viewed in a web browser. But since version 4.0, `plotly` is offline only, which means all figures are rendered in the local environment. Even if figures are displayed in a web browser window, the figure does not exist online--the web browser is loading a figure from the local environment.

  * For more on `plotly`'s move to offline-only: plotly, ["Plotly.py 4.0 is here: Offline Only, Express First, Displayable Anywhere"](https://medium.com/plotly/plotly-py-4-0-is-here-offline-only-express-first-displayable-anywhere-fc444e5659ee) *Medium* (22 July 2019).

## Static Image export

We can export `plotly` figures as static image file formats (`.png`, `.jpeg`, `.svg`, and `.pdf`). Static image generation requires the [`Kaleido` package](https://github.com/plotly/Kaleido).

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

<blockquote>Q3: Add to the code for at least one of the figures generated earlier in this lab to save the figure as a static image. Include code + comments.</blockquote>

## Saving to HTML

We can also export `plotly` figures as `HTML` files which can be loaded in a web browser. Unlike static image exports, these `HTML` files will include the interactivity of the `plotly` figure. Once a figure has been created, we can use the `.write_html()` method to save the figure as an `HTML` file.

```Python
# save to html
fig.write_html("filepath/filename.html")
```

For more on HTML file export: [`plotly`, Interactive HTML Export in Python](https://plotly.com/python/interactive-html-export/)

<blockquote>Q4: Add to the code for at least one of the figures generated earlier in this lab to save the figure as an HTML file. Include code + comments.</blockquote>

## `dash`

`plotly` figures can also be part of an interactive web app built using `dash`. [For more on getting started with `dash`](https://github.com/kwaldenphd/dash-python/)

# Lab Notebook Questions

[Link to access the lab notebook template (Jupyter Notebook)](https://drive.google.com/file/d/1J4UZ0HBBSQYzTjbzAelzfwgSZ-YIdKeN/view?usp=sharing)

Q1: Build at least three different types of plots using plotly and data stored in a Pandas DataFrame. Include code + comments.
- *I encourage folks to use this question to explore visualizations you might use for the final project.*

Each plot should include the following elements:
- Title
- Axis labels
- Legend
- Scale or tickmarks
- Hover label
- Data source
 
Plot types to choose from:
- Line plots
- Bar chart
- Grouped bar chart
- Horizontal bar chart
- Stacked bar chart
- Histogram
- Box plot
- Area plot
- Scatter plot
- Pie chart
- Donut chart
- Sunburst chart
- Table

Q2: Build at least two different types of maps using plotly. Include code + comments.
- *I encourage folks to use this question to explore visualizations you might use for the final project.*

Each plot should include the following elements:
- Title
- Hover labels
- Scale
- Data source

Types of maps to choose from:
- Geo Maps, or Outline-Based Maps
  * Point map, `px.scatter_geo()`
  * Choropleth map `px.choropleth()`
- Mapbox or Tile-Based Maps
  * Point map, `px.scatter_mapbox()`
  * Choropleth map, `px.choropleth_mapbox()`

Q3: Add to the code for at least one of the figures generated earlier in this lab to save the figure as a static image. Include code + comments.

Q4: Add to the code for at least one of the figures generated earlier in this lab to save the figure as an HTML file. Include code + comments.
