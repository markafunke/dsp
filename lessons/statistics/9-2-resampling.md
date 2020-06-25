[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

## QUESTION
In Section 9.3, we simulated the null hypothesis by permutation; that is, we treated the observed values as if they represented the entire population, and randomly assigned the members of the population to the two groups.

An alternative is to use the sample to estimate the distribution for the population, then draw a random sample from that distribution. This process is
called resampling. There are several ways to implement resampling, but one of the simplest is to draw a sample with replacement from the observed values, as in Section 9.10.

Write a class named DiffMeansResample that inherits from DiffMeansPermute and overrides RunModel to implement resampling, rather than permutation.

Use this model to test the differences in pregnancy length and birth weight. How much does the model affect the results?


## SOLUTION

#### Override RunModel to sample from each group instead of permutation
```python

class DiffMeansResample(DiffMeansPermute):
    """Tests a difference in means using resampling."""
    
    def RunModel(self):
        """Run the model of the null hypothesis.

        returns: simulated data
        """
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        return group1, group2
 ```

#### Test differences in pregnancy length and birth weight using resampling
```python
#Prepare Length dataset and calculate p_values
data_length = firsts.prglngth.values, others.prglngth.values
ht_length = DiffMeansResample(data_length)
p_value_length = ht_length.PValue(iters=10000)

#Results
p_value_length
```
0.1651

```python
#Prepare Weight dataset and calculate p_values
data_weight = (firsts.totalwgt_lb.dropna().values,
        others.totalwgt_lb.dropna().values)
ht_weight = DiffMeansResample(data_weight)
p_value_weight = ht_weight.PValue(iters=10000)

p_value_weight
```
0.0001

The model did not change results much, as the p-values are very similar for both length and weight, and we can't reject the null for length, but can for weight.



