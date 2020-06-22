[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

## EXERCISE
Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?**

## SOLUTION

### Prep Data
```python
#load in pregnancy dataframe
preg = nsfg.ReadFemPreg()

#limit to just live births
live = preg[preg.outcome == 1]

#separate live births into first and all others
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]
```
### Calculate Results
```python
#calculate means of each group
firsts_mean = firsts['birthwgt_lb'].mean
others_mean = others['birthwgt_lb'].mean
firsts_mean, others_mean
```
(6.752968036529681, 6.905824829931973)

```python
#calculate cohens d
CohenEffectSize(firsts['birthwgt_lb'], others['birthwgt_lb'])
```
-0.10845024254407831

Cohen's d for length was 0.0289, which is the opposite direction and a much smaller difference than the -0.109 for birthweight.
