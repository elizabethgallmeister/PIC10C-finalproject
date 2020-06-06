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

**May 27:** I spent a fair bit of time today looking for a good dataset for COVID-19 data.

The best one that I found is [here](https://github.com/owid/covid-19-data/tree/master/public/data/), and I think it'll serve its purpose well because it has an abundance of information. Of the 32 columns, some that I thought would be very helpful were `location`, `population`, and `population_density` for making a map overlay, `total_cases`, `new_cases`, `total_deaths`, `new_deaths`, and variables of that sort which could be good for projections of when the peak is/was, or how the future may look. And then there were also interesting characteristics that I could examine later to see if I could project more specific outcomes for different people in different situations, such as `median_age`, `extreme_poverty`, `male_smokers`, `female_smokers`, etc.

One *problem* that I forsee is because of the fact that this data is being updated daily. I plan to use the dataset downloaded today, May 27, to start all of the skeletal code for mapping, forecasting, and analyzing, but I think it will be a challenge to go back to the updated dataset, especially if new columns have been implemented, or some huge change has been made.

I also found a dataset from Johns Hopkins that could be helpful [here](https://www.kaggle.com/imdevskp/corona-virus-report), but it definitely isn't as informative as the above example.

**May 31:** Started working with the actual coronavirus dataset. Ran into two main issues:

* Making graphs was a really huge struggle because of the huge size of the dataset, and I wasn't sure exactly what I wanted to convey. I kind of shelved that issue for another day and focused just on the United States COVID-19 data.
* I really wanted to put the United States total_cases and total_deaths on the same graph, as the x and y axes were measuring the same variables and I wanted to see whether the death rate was decreasing or increasing, then see if I could attribute that to **(1)** more testing leading to a lower, or possibly higher, relative death rate, **(2)** an increase in death rate as hospitals ran out of supplies / respirators / etc, or **(3)** a decrease in death rate as hospitals began to receive resources (although I'm not fully sure this ever actually happened :/ ...)

**June 3:** After thinking over it, I think I've come up with my next step and some goals, given the size of my dataset. 
1. I want to get the overlaid graphs of total_cases and total_deaths working
2. I'd like to create graphs like the ones made earlier of the United States cases for other countries whose rise and fall already occurred, like maybe Italy and China (places that were middle of the road in peak like Italy, and places where it was a huge issue much earlier, like China). I'd like to stack them vertically to see the differences in where the peaks were vs. when the first case occurred.
3. I want to create a time series forecasting/prediction of the United States data, up to the date I got the dataset (May 27), then compare it to how the dataset looks near the end of finals week, 2 weeks later.
4. I'd also like to create time series predictions for Italy and China, but only using the first, say, 2/3 of their data and then compare that to the actual progression of the virus.

In terms of what I worked on today, I tried a few different things to make an overlaid bar graph or other overlaid graphs that would show total_cases and total_deaths in the US. And again, failed. But, I found a resource that I thought would be useful to come back to next time.

**June 5:**

* I had an issue where the cell `temp.drop(['relative_deaths'], axis = 1)` kept giving me an error and I couldn't understand why, but I realized that it's because I never created the `relative_deaths` column when I recompiled all of the cells upon logging on today, so it was trying to drop a column that didn't exist. That's definitely one of the parts of Jupyter Notebook that I'm still getting used to.

* The next issue was the next cell, which graphed relative deaths two days ago. Now it's giving me the error: `ValueError: Could not interpret input 'relative_death'` which I'm currently trying to figure out how to fix. relative_death is the column name of temp, so I'm not sure what's going wrong.
* UPDATE: I tried printing temp because obviously for whatever reason, the column that I had created wasn't being registered. And lo and behold, the relative_deaths column was gone. I read up on `assign`, which I used to create the column, and saw that "Existing columns that are re-assigned will be overwritten" [Source](https://www.geeksforgeeks.org/python-pandas-dataframe-assign/#:~:text=Dataframe.,of%20rows%20in%20the%20dataframe.). So, what I think is happening is because I call `assign`, which creates a new dataframe, but I'm not really saving it anywhere, it's just getting lost.
* What I did: I assigned the copied dataset to a variable called temp2: `temp2 = temp.assign(relative_death=temp['total_deaths']/temp['total_cases'])`

* I then referenced the [link](https://stackoverflow.com/questions/52952857/how-to-plot-stacked-bar-chart-using-one-of-the-variables-in-pandas) I left in my Notebook to try and overlay the bar graph the way I want using a pivot table.
* Original code: 
        
        s = (df.pivot_table(index='City_Category', columns='Gender', values='Purchase', aggfunc='sum'))
        s.plot(kind='bar', stacked=True)
        plt.show()
        
* For mine, index should be 'date', columns should be deaths and cases in the same way that gender has male and female, values should be total_deaths and total_cases. Now to reconfigure my dataframe to reflect this...
* Okay never mind, because I just realized that this graph would add the number of deaths to the number of cases, which isn't what we wanted either (the assumption being that deaths started as confirmed cases).
* In addition, I don't think there's a way to make my dataset resemble the form that would be needed to do this. This is because in the case of the example, male and female were independent of their purchasing, whereas there's no way to say 'total_deaths' and 'total_cases' on a specific day would be in the deaths category, and a different day would be in the 'cases' category.
* I tried one last Google search and came across [this thread](https://stackoverflow.com/questions/23293011/how-to-plot-a-superimposed-bar-chart-using-matplotlib-in-python), which helped me finally create a stacked bar graph. It was highly underwhelming, though, because the death rate is so tiny compared to the rate of cases. 

* Next up: Creating graphs of other countries (Italy and China to start), then stacking them vertically to see the differences in their timelines.
* This is where I realized that not only does the dataframe start after China's first case, but also total_cases never decreases. You can see this in the graph for China's total cases-- it flattens out near the end of March. Meaning, even if people die or recover, that doesn't decrease total_cases. This means at first glance that I can't measure where the peak was, especially because there's no variable for recovery.
* Or is there? If I graph based on new cases? Not sure - I'll think on it and come back to it.
