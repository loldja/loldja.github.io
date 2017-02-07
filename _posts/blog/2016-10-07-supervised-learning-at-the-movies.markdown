---
layout: post
title: "Supervised Learning at the Movies"
date: 2016-10-07 18:40:46
author: "Lauren Oldja"
categories:
- blog
- machine-learning
img: movies-linear-regression.png
thumb: metis-logo.gif
---

For those following along here or on [my Twitter](http://www.twitter.com/urbanplans) account it's no secret that I am currently enrolled at [Metis](http://www.thisismetis.com) in their 12-week data science bootcamp, which marries the structure of daily morning problem solving with highly self-guided and project-based afternoons/evenings/weekends. The expectations are high, and the deadlines are "intentionally unfair", giving the three months a hackathon-lite vibe. Some projects featured on this blog, this post included, accompany projects completed and presented for Metis. For this project I scraped [Box Office Mojo](http://www.boxofficemojo.com) in order to build a predictive linear regression model.<!--more-->

## Analysis
At first blush, predicting domestic box office gross is hardly worthy of machine learning: instinctively we know it must be a function of increasing marketing and production budgets. In other words, "Money In, Money Out (MIMO)". But what else might have an effect?

I scraped information on budget, MPAA rating, runtime, genre, and release date for five years (2011-2015) of worldwide releases from BoxOfficeMojo using [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) and Python 3.4 Anaconda distribution with pandas. I focused on the mass-market viable movies only by restricting the analysis to PG, PG-13, and R rated movies; G rated movies were removed since they are marketed and consumed in a very different way, such as requiring toy tie-ins.

In addition to reading in these features, I created new features that were interaction terms of budget and genre multiplied together. Multiplying budget by every unique genre generated too many features to be useful (and this complexity made the model at risk of overfitting), but I did supect that budget would affect different genres differently -- a big budget for an action movie may help make it a blockbuster in a way that a mystery or chick-flick could never be. I used a lasso regularization to reduce my model to the most significant features.

In a linear regression, the R-squared term is a measure of "goodness of fit", and in this case the resulting model had an R-squared of 0.502, which means that just over 50% of the variation among the observed data can be explained by the results OLS regression model. The underlying distribution of the data is unlikely to be linear in nature, which limits our ability to improve R-squared substantially, however in order to improve the model, my next step would be to create interaction terms for runtime versus genre (I suspect in general there is a overall optimal runtime for movies, but that perhaps audiences will expect fantasy movies to be longer than action movies of similar budgets) and to scrape more years of worldwide movie releases so that we are expanding our label-space at the same time as we add more features.

## Download my code
My slides and codebase are available on [Github](https://github.com/loldja/ds9_luther), and as ever [feedback is welcome](http://www.laurenoldja.net/contact). 
