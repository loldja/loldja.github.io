---
layout: post
title: "Survival Analysis to Explore Customer Churn in Python"
date: 2018-04-10 18:40:46
author: "Lauren Oldja"
categories:
- blog
- survival-analysis
img: survival.png
thumb: metis-logo.gif
---
Originally posted in the online publication ["Towards Data Science" on Medium](https://towardsdatascience.com/survival-analysis-in-python-a-model-for-customer-churn-e737c5242822)

---

Survival analysis refers to a suite of statistical techniques developed to infer <i>“lifetimes”</i>, or time-to-event series, without having to observe the event of interest for every subject in your training set. The <i>event of interest</i> is sometimes called the subject’s <i>“death”</i>, since these tools were originally used to analyze the effects of medical treatment on patient survival in clinical trials.<!--more-->

Meanwhile, <i>customer churn</i> (defined as the opposite of <i>customer retention</i>) is a critical cost that many customer-facing businesses are keen to minimize. There is [no silver bullet methodology](https://www.kdnuggets.com/2017/03/datascience-building-predictive-churn-model.html) for predicting which customers will churn (and, one must be careful in [how to define whether a customer has churned for non-subscription-based products](https://www.datascience.com/blog/intro-to-predictive-modeling-for-customer-lifetime-value)), however, <i>survival analysis</i> provides useful tools for exploring time-to-event series.

## Why can’t we just use OLS linear regression?

OLS works by drawing the regression line that minimizes the sum of the squared error terms. With unobserved data, however, the error terms cannot be known, and therefore it would be impossible to minimize these values.

Simply taking the date of censorship to be the effective last day known for all subjects, or worse dropping all censored subjects can bias our results.

![Not all deaths have been observed by t1, the time of observation.](/assets/img/blog/censorship.png)

In the graphic above, U002 was censored from loss to follow-up (perhaps due, for example, to an unresolved technical issue on the account that left the customer’s status unknown at the time of the data pull), and U003 and U004 are censored because they are current customers. As of <i>t1</i>, only U001 and U005 have both observed birth and death. As the graphic makes clear, dropping unobserved data would under-estimate customer lifetimes and bias our result.

---

Survival analysis handles event <i>censorship</i> flawlessly. A customer who has been censored is one whose death has not been observed. The main way this could happen is if the customer’s lifetime has not yet completed at the time of observation. (N.B. In clinical trials, patients who have been <i>lost to follow-up</i> or dropped out of the study are also considered censored.)

## Kaplan-Meier curves

For any problem where every subject (or customer, or user) can have only a single “birth” (enrollment, activation, or sign-up) and a single “death” (regardless of whether it is observed or not), the first and best place to start is the Kaplan-Meier curve. This will allow us to estimate the “survival function” of one or more cohorts, and it is one of the most common statistical techniques used in survival analysis.

Survival analysis can be used as an exploratory tool to compare the differences in customer lifetime between cohorts, customer segments, or customer archetypes. In Python, we can use Cam Davidson-Pilon’s [lifelines](https://github.com/CamDavidsonPilon/lifelines) library to get started.

Take, for example, this [IBM Watson telco customer demo dataset](https://www.ibm.com/communities/analytics/watson-analytics-blog/predictive-insights-in-the-telco-customer-churn-data-set/). By segmenting on the binary feature for single versus multiple phone lines, we get the following Kaplan-Meier curves.

![Customers with one phone line have a steeper survival curve initially, but by ~4 years 3 months customer lifetime the error bars make the two groups indistinguishable.](/assets/img/blog/k-m.png)

We can see that 1 in 4 users have churned by month 25 of those who have only one phone line. By comparison, 1 in 4 users churn by month 43 among those with multiple phone lines, for a difference of 18 months (an extra 1.5 years of revenue!)

Correlation is not causation, and therefore this graph alone cannot be considered “actionable”. We may, however, look at this and begin to suspect some possibilities, such as that customers with multiple phone lines are more “locked in” and therefore less likely to churn than single phone line users. On the other hand, perhaps customers who are more loyal tend to prefer multiple phone lines in the first place.

And who should get more investment? If the two groups are equally profitable, it may be worth spending more to keep the single phone line users happy, since they currently tend to churn more quickly. Or, an experimental design could reveal that some incentives double lifetimes for <i>all customers</i>, and since the lifetimes of multiple line users tend to be longer originally, this multiplying effect actually would be more profitable for that segment.

Without more context, and possibly experimental design, we cannot know for sure.

## Pros and Cons of Kaplan-Meier Curves

### Pros:

- Minimal feature set needed. Kaplan-Meier only needs the time which event occurred (death or censorship) and the lifetime duration between birth and event.
- Many time-series analyses are tricky to implement. Kaplan-Meier only needs all of the events to happen within the same time period of interest
- Handles class imbalance automatically (any proportion of deaths-to-censored events is okay)
- Because it is a non-parametric method, few assumptions are made about the underlying distribution of the data

### Cons:

- Cannot estimate the magnitude in difference of the survival-predictor relationship of interest (no hazard ratio or relative risk)
- Cannot account for multiple factors simultaneously for each subject in the time to event study, nor control for confounding factors
- Assumes independence between censoring and survival, meaning that at time t, those who have been censored should have the same prognosis as those who have not been censored.
- Because it is a non-parametric model, it is not as efficient or accurate as competing techniques on problems where the underlying data distribution is known

## Now try it yourself!

To see how I made this Kaplan-Meier plot and to get started with your own survival analysis, download the [jupyter notebook](https://github.com/loldja/loldja.github.io/blob/master/assets/code/blog/Kaplan%20Meier%20demo.ipynb) from my Github account.
