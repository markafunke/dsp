[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

## QUESTION
Exercise 5.1 In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ =7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

## SOLUTION
To find the percentage of the population in this range we need to take the cdf at 6'1" - the cdf at 5'10".

```python
import scipy.stats


#create function to convert blue man group heights to centimeters
def feet_in_to_cm(feet,inches):
    '''
    Converts feet/in height to centimeters
    
    Parameters
    ----------
    feet : integer
    inches : float

    Returns
    -------
    cm : float

    '''
    INCHES_TO_CM = 2.54
    total_inches = feet*12 + inches
    cm = total_inches * INCHES_TO_CM
    return cm

low_cm = feet_in_to_cm(5,10)
high_cm = feet_in_to_cm(6,1)

#paramters from exercise
mean_men = 178.0 
std_men = 7.7

#calc cdf for low and high range
low_blue = scipy.stats.norm.cdf(x= low_cm,loc = mean_men, scale = std_men)
high_blue = scipy.stats.norm.cdf(x= high_cm,loc = mean_men, scale = std_men)

#final percent of men in height range
US_blue_man_percent = high_blue - low_blue
```
US_blue_man_percent --> 0.34274683763147457
