[Think Stats Chapter 8 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

## QUESTION
Suppose you draw a sample with size n = 10 from an exponential distribution with λ = 2. 

Simulate this experiment 1000 times and plot the sampling distribution of the estimate L. 

Compute the standard error of the estimate and the 90% confidence interval.

Repeat the experiment with a few different values of n and make a plot of standard error versus n.

## SOLUTION

#### Simulate
```python
#define functions for estimating exponential, and calculate RMSE
def Estimate_Exp(n, m, lam):
    """Evaluates L as estimators of the exponential parameter.

    n: sample size
    m: number of iterations
    lam: exponential parameter
    """

    means = []
    
    for i in range(m):
        xs = np.random.exponential(1/lam, n)
        L = 1 / np.mean(xs)
        means.append(L)
        
    return means


def RMSE(estimates, actual):
    """Computes the root mean squared error of a sequence of estimates.

    estimate: sequence of numbers
    actual: actual value

    returns: float RMSE
    """
    e2 = [(estimate-actual)**2 for estimate in estimates]
    mse = np.mean(e2)
    return math.sqrt(mse)
    
#run simulation
n7 = Estimate_Exp(n=7,m=1000,lam=2)
```

#### Compute standard error 
```python
stderr = RMSE(n7, 2)
```
1.3072557065336807

#### Compute 90% CI
```python
ci = cdf.Percentile(5), cdf.Percentile(95)
```
(1.1562026444305387, 4.25826605665103)

#### Repeat with different "n". Plot standard error vs n.
```python
#create dataframe to store n/RMSE values for all n from 5 to 50
df = pd.DataFrame(columns=['n', 'RMSE'])
for n in range(5,50):
    df = df.append({'n':n, 
                    'RMSE': RMSE(Estimate_Exp(n,m=1000,lam=2),2),
                    }, ignore_index=True )

#plot n vs RMSE to test how increasing n changes RMSE
RMSEs = df['RMSE']
ns = df['n']    
thinkplot.Scatter(ns, RMSEs)
thinkplot.Show(xlabel='n',
ylabel='RMSE',
axis=[5, 50, 0, 2])
```
Can see as n increases, RMSE trends towards 0.
![RMSE plot](https://github.com/markafunke/dsp/blob/master/lessons/statistics/RMSE_plot.png).
