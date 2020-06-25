[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

## QUESTION

In games like hockey and soccer, the time between goals is roughly exponential. So you could estimate a team’s goal-scoring rate by observing the number of goals they score in a game. This estimation process is a little different from sampling the time between goals, so let’s see how it works.

Write a function that takes a goal-scoring rate, lam, in goals per game, and simulates a game by generating the time between goals until the total time
exceeds 1 game, then returns the number of goals scored.

Write another function that simulates many games, stores the estimates of lam, then computes their mean error and RMSE.

Is this way of making an estimate biased? 
Plot the sampling distribution of the estimates and the 90% confidence interval. 
What is the standard error?
What happens to sampling error for increasing values of lam?

## SOLUTION

#### Simulate Game Functions
I admittedly struggled with this one, and walked through Think Stats example solution for the functions needed.
* The first function, SimulateGame, uses a random exponential variable to simulate the time between goals, and estimates goals scored in a single game, or t = 1
* The second function runs this Simulation m times and stores the estimates in a list, then calculates error and plots the PMF along with a 90% CI

def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L


def SimulateGames(lam, m):

    estimates = []
    for i in range(m):
        L = SimulateGame(lam)
        estimates.append(L)

    print('rmse L', RMSE(estimates, lam))
    print('mean error L', MeanError(estimates, lam))
    
    cdf = thinkstats2.Cdf(estimates)
    ci = cdf.Percentile(5), cdf.Percentile(95)
    VertLine(ci[0])
    VertLine(ci[1])
    
    pmf = thinkstats2.Pmf(estimates)
    thinkplot.Hist(pmf)
    thinkplot.Config(xlabel='Goals scored', ylabel='PMF')


#### Insights
* Not biased, as error is trending towards 0 as we increase the amount of games
* RMSE is 1.73 for a lambda of 3 and 100,000 games
* As lambda increases, error increases, 
as a higher lambda means fewer time between goals, and more goals, which will lead to more error estimating larger numbers
