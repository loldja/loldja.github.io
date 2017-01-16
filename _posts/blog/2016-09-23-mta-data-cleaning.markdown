---
layout: post
title: "Data Cleaning and the MTA: Part 1"
date: 2016-09-23 18:40:46
author: "Lauren Oldja"
categories:
- blog
- open-data
img: mta-data-cleaning.gif
thumb: metis-logo.gif
---

Apocryphally, [80% of data science is data munging](https://www.thoughtworks.com/insights/blog/let-data-scientists-be-data-mungers), i.e. cleaning the data into a usable format. If you want to use Pandas on the NYC MTA Subway turnstile data, here's some steps to get you started. Don't miss the iPython/jupyter notebook I've included at bottom of the post.<!--more-->

As part of the [NYC Open Data initiative](https://data.ny.gov/), the Metropolitan Transit Authority makes available the raw turnstile data on a weekly basis from mid-2010 to Present. You can download these direct from the [MTA website](http://web.mta.info/developers/turnstile.html). Open up a recent file. How can we transform real-world data into something more user-friendly?

## Tutorial  

Tools used: Python 2.7; pandas; jupyter notebook  

### Import the CSV data into pandas DataFrame
{% highlight python %}
datafiles = ['data/mta_turnstiles/' + x for x in os.listdir('data/mta_turnstiles/')]

list_ = []
for file_ in datafiles:
    df = pd.read_csv(file_)
    list_.append(df)
df = pd.concat(list_)
{% endhighlight %}
Doing so in this way means that it will append any number of files from the data/ folder, instead of hard-coding the filename directly.

### Strip the whitespace from column headers
{% highlight python %}
df.columns = df.columns.str.strip()
{% endhighlight %}
This, like dropping duplicates, is generally a good idea when you are getting external data and don't know how messy it's going to be. In our case, many of the MTA CSVs have trailing strings after 'EXIT' in the columns headings.

### Make a usable timestamp
{% highlight python %}
df['TIMESTAMP'] = pd.to_datetime((df.DATE + ' ' + df.TIME), format='%m/%d/%Y %H:%M:%S')
{% endhighlight %}
Instead of two columns with date and time separately stored as strings, now you have a single datetime object.

### Create unique identifiers per station
{% highlight python %}
df = df.reset_index()
l = [''.join(sorted(a)) for a in df['LINENAME']]
df['STATID']=df['STATION']+pd.Series(l)
{% endhighlight %}
By sorting the line name first, you avoid the problem of creating two or more unique identifiers per station in the case that the order of lines is changed for stations serving multiple lines.

### Recognize that turnstiles are cumulative counts
{% highlight python %}
df['ENTRY_DIFF']=df.groupby(['STATID','UNIT','SCP'],as_index=False)['ENTRIES'].transform(pd.Series.diff)['ENTRIES']
{% endhighlight %}
<<<<<<< HEAD
Since the numbers are in the millions and generally keep climbing, we can be fairly confident in making this assumption. We need to take a row-by-row difference in order to get entry counts for the intervals.
=======
Since the numbers are in the millions and generally keep climbing, we can be fairly confident in making this assumption. We need to take a row-byrow difference in order to get entry counts for the intervals.
>>>>>>> 20915954873b969eef46936624ca1d92afc43afc

### Make hourly bins
{% highlight python %}
df['HOD'] = [r.hour for r in df.TIMESTAMP] #hod = "hour of day"
df['HODBIN'] = pd.cut(df['HOD'], bins)
{% endhighlight %}
Turnstile entry counts are taken approximately at 4hr intervals, although these are not the same for each station. Simplify this issue by binning your data. You could also use a simple linear model to interpolate the entries/exits for comparability.

## Download notebook  

[Here's a link](https://github.com/loldja/loldja.github.io/blob/master/assets/code/blog/mta_cleaning.ipynb) to a jupyter notebook to take you through these steps and a few more to get you started. In Part Two (coming soon!) I'll suggest some techniques for exploratory data visualization and treatment of outliers. 

Until then... happy cleaning, everyone!
