# PIC10C-finalproject

This is my final project for PIC 10C; it's my learning how to use Jupyter Notebook and Python to do data analysis.
I started by learning how to use Jupyter with some tutorials, then went on to analyze a dataset that I found interesting.

Here's a general log of what I did:

**May 17:** To download Jupyter Notebook, I first had to download Miniconda. I ran into some issues with local repositories
and creating my folder, but eventually got both downloaded and working.

**May 18:** Initial Commit & Hello, World in Jupyter Notebook

**May 19:** Reviewed some Markdown and started this README! I also planned how I would be breaking up the tutorials I was going to follow.
They can be found here:
1. [Munging Data](http://wavedatalab.github.io/datawithpython/munge.html)
2. [Aggregating Data](http://wavedatalab.github.io/datawithpython/aggregate.html)
3. [Visualizing Data](http://wavedatalab.github.io/datawithpython/visualize.html)
4. [Time Series](http://wavedatalab.github.io/datawithpython/timeseries.html)

As I went through the tutorials, I logged my main takeaways in the notebook itself, as well as noted topics I wanted to further investigate.

**May 20:** First tutorial: Munging Data

**May 21:** Investigating `ix` vs `loc` vs `iloc` ([Source 1](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.ix.html), [Source 2](https://www.youtube.com/watch?v=naRQyRZrXCE))

`ix`:
* outdated as of 0.20.0
* primarily label-based indexer, but had integer backup
* supports mixed integer and label based access
* `loc` and `iloc` are generally more strict

`loc`:
* creates subset of data using row and column *names* as parameters
* for all members of a certain column, call `df.loc[:,'name_of_col']` or for multiple columns: `df.loc[:,[col1,col2]]`
* can also be used to filter entries within a column: `df.loc[df.col_name == "col_value"]`
* ranges are inclusive for first and second values

`iloc`:
* used for filtering rows and selecting columns based on *integer* values
* for first two columns of a dataset, call `df.iloc[:,0:2]`
* ranges are inclusive of first value and exclusive of second

**May 23:** Second tutorial: Aggregating Data

Investigating the `lambda` funtion ([Source](https://www.w3schools.com/python/python_lambda.asp))
* `lambda` functions are anonymous functions that take any number of parameters and contain one expression
* in following the tutorial, I wrote the line `criterion = cereal['name'].map(lambda x: x.startswith('A'))`
* the above line of code goes through each entry in the 'name' column, represented as x, and calls `x.startswith('A')`
* this function was actually a lot more simple than I thought, and I think it'll be something I'll learn to implement often

**May 24:** Third tutorial: Visualizing Data

**May 25:** Investigating Seaborn ([Source](https://seaborn.pydata.org/))
* Seaborn: a Python data visualization library to draw statistical graphics, based on matplotlib
* When statistical values are estimated, it uses bootstrapping to compute confidence intervals and draw error bars representing the uncertainty of the estimate.
* `catplot()` is used for visualizing the relationship between a numerical value and 1+ categorical variable, and `relplot()` is for visualizing the relationship between numerical values
* Axes-level functions takes `ax=` argument and return the matplotlib `axes`
* Figure-level functions don't take the `ax=` arg and return the `FacetGrid`
* To visualize multiple plots, can use `joinplot()`, which focuses on a single relationship, or `pairplot()`, which shows all pairwise relationships and the marginal distributions

**May 26:** Brainstorming for the "Official" bit of my final project
* I think it would be interesting to analyze Coronavirus data, or if it's not excessively available, another disease/virus. Things I can do with virus data:
* Make different graphs to visualize the data
* Map data coordinates to a graphic
* Use time series to make a forecast, of infection/death/recovery
* I could start with a different virus data to see the accuracy of the time series predictions, and see if I could improve it somehow
