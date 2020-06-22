[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

## QUESTION
Exercise 3.1 Something like the class size paradox appears if you survey
children and ask how many children are in their family. Families with many
children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.
Now compute the biased distribution we would see if we surveyed the children
and asked them how many children under 18 (including themselves) are in
their household.
Plot the actual and biased distributions, and compute their means. As a
starting place, you can use chap03ex.ipynb.

## SOLUTION
#### Construct actual distribution for the number of children under 18 in the household
```python
kid_pmf_actual = thinkstats2.Pmf(resp['numkdhh'], label = 'actual')
```

#### Compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household
```python
#use BiasPmf function from book
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf

kid_pmf_biased= BiasPmf(kid_pmf_actual, label = 'biased')
```

#### Plot the actual and biased distributions, and compute their means
```python
#create bar chart of pmf for both biased and unbiased
actual_hist = thinkstats2.Hist(kid_pmf_actual)
biased_hist= thinkstats2.Hist(kid_pmf_biased)

#plot charts side by side
width = 0.45
thinkplot.PrePlot(2)
thinkplot.Hist(actual_hist, align='right', width=width)
thinkplot.Hist(biased_hist, align='left', width=width)
thinkplot.Show(xlabel='kids in family', ylabel='pmf')
```

![Valid XHTML](https://github.com/markafunke/dsp/blob/master/lessons/statistics/kids_biased_unbiased.png).

```python
kid_pmf_actual.Mean()
kid_pmf_biased.Mean()
```
actual mean = 1.024
biased mean = 2.404



