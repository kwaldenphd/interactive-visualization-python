# Interactive Visualization in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

This lab provides an overview of interactive data visualization in Python using `plotly`. It provides an overview and comparison of the `bokeh` and `plotly` packages. It provides an overview of `plotly` functionality, focusing on `plotly.express` functions for a variety of plot types, including 2D cartesian coordinate system plots and mapping using geospatial data. It ends with an overview of export options for `plotly` figures.

By the end of this lab, students will be able to:
- Understand the basic components of interactive Python visualization packages `bokeh` and `pandas`
- Understand the basic syntax used to generate a `plotly` figure for a variety of plot types, using `plotly.express` functions
- Understand the syntax and options available for customizing a `plotly` figure
- Understand the export options for a `plotly` figure
- Be able to use `plotly.express` functions to generate their own figures, with a basic level of customization
- Understand how to navigate and interact with `plotly` documentation for tutorials and troubleshooting

## Acknowledgements

The author consulted the following resources when writing  this tutorial:
- [`plotly` documentation and tutorials](https://plotly.com/python/)

# Table of Contents

- [Lab notebook template](#lab-notebook-template)
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

# Lab Notebook Template

[Link to access the lab notebook template (Jupyter Notebook)](https://drive.google.com/file/d/1J4UZ0HBBSQYzTjbzAelzfwgSZ-YIdKeN/view?usp=sharing)
