---
title:"Non-Parametric Estimation Approaches"
layout: post
---
Non-Parametric Estimation and Bootstrapping; data-driven approaches where distributions are not specified.

# Non-Parametric Approaches
Parametric forms of estimation make very specific assumptions about distributions of data - for example, the assumption of a Normal or Lognormal distribution. Non-Parametric approaches use empirical data to drive the distribution's classification.

## Bootstrap Historical Simulation
If Historical Simulation is the process of calculating VAR from a historical dataset, then the Bootstrap Historical Simulation method can be thought of as repeated Historical Simulation.

## Improvements to the Historical VAR Simulation Method

### Age-Weighted Historical Simulation
An issue with Historical VAR is the concept that...why are all data points in the data set equally relevant? Why is the 95th data point important but the 96th is not, for example. Age-Weighting solves this issue, albeit in a simplistic way, by gradually reducing the weight of data points as we step back in time.

$w(i) = \frac{\lambda^{i-1}(1-\lambda)}{1-\lambda^n}$

Where $\lambda$ is the decay factor, and $0<=\lambda<=1$. So for example w(1) would be $\lambda$ and w(2) would be $\lambda^2$. 

### Volatility-Weighted Historical Simulation
This method weights values either up or down based on the volatility at the time (via GARCH or EWMA). This serves to account for time-varying volatiity characteristics, to ensure that our VAR is not under or overestimated. 

$r_{t,i} = \left ( \frac{\sigma_{T,i}}{\sigma_{t,i}} \right )r_{t,i}$

Where...
$r_{t,i}$ = the actual return for asset i on day t
$\sigma_{t,i}$ = volatility forecast for asset i on day t (made at the end of day t-1)
$\sigma_{T,i}$ = current forecast of volatility for asset i

So for example if Volatility is currently 1 and was 0.5 on the day of the observation, we will multiply the value from that particular day by 2 (1/0.5). This allows for VAR estimates which are higher than the vanilla Historical Method.

### Correlation-Weighted Historical Simulation
Correlation (or variance covariance) weighting is similar to Volatility weighting but applied to the correlation between assets in a portfolio.

### Filtered Historical Simulation
This is a comprehensive approach in which - for each data point - conditional volatility models are applied, and standardisation is performed by dividing the datapoint by realised returns. Bootstrapping is used to simulate returns which incorporate current volatility levels.

# Advantages and Disadvantages

The advantages are that non-parametric methods are simple, flexible and avoid complicated variance-covariance matricies and the likes. Furthermore we can apply time, volatility, and correlation-based weighting regimes on existing data relatively easily. 

The disadvantages, however, are that non-parametric methods are highly dependant on data. Therefore if data exhibits characteristics which are either too high or too low, then our estimates will be misleading. Non-parametric methods will not be able to detect regime changes, and of course, if an instrument is new, we won't have any historical data to use at all.
