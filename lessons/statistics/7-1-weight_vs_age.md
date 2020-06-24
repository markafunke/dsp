[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

## QUESTION
Using data from the NSFG, make a scatter plot of birth weight versus mother’s age. 

Plot percentiles of birth weight versus mother’s age.

Compute Pearson’s and Spearman’s correlations. 

How would you characterize the relationship between these variables?

## SOLUTION
#### Scatterpolot of birth weight vs. mother's age
```python
ages = live['agepreg']
weights = live['totalwgt_lb']

thinkplot.Scatter(ages, weights, alpha=0.5, s=5)
thinkplot.Config(xlabel='Age (years)',
                 ylabel='Weight (lbs)',
                 legend=False)
```
![Image of Scatterplot](https://github.com/markafunke/dsp/blob/master/lessons/statistics/ages_weight_scatter.png)


#### Percentiles of birth weight vs. mother's age
![Image of Scatterplot](https://github.com/markafunke/dsp/blob/master/lessons/statistics/percentiles_plot.png)

#### Correlations
```python
Corr(ages, weights), SpearmanCorr(ages, weights)
```
(0.06883397035410908, 0.09461004109658226)

#### Findings
The scatterplot and correlations show no meaningful relationship between the age of the mother and the weight of the child.
The binned percentiles show a linear increase early on (ages 15 to about 25, then no impact.
