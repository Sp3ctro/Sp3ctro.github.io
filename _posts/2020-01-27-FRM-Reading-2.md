---
title: "Non-parametric VAR Approaches"
layout: post
---
Non-Parametric VAR Estimation and Bootstrapping; data-driven approaches in which distributions are not specified, and data are embellished.

# Non-Parametric VAR Approaches
Parametric forms of estimation make very specific assumptions about distributions of data - for example, the assumption of a Normal or Lognormal distribution. Non-Parametric approaches use empirical data to drive the distribution's classification.

## Bootstrap Historical VAR Simulation
*LO 2a: Apply the bootstrap historical simulation approach to estimate coherent risk measures*

If Historical Simulation is the process of calculating VAR from a historical dataset, then the Bootstrap Historical Simulation method can be thought of as repeated Historical Simulation. With this method, we take repeated samples from the dataset, compute a Historical VAR, a "replace" the values back into the dataset. The term "replace" means that random samples are chosen repeatedly, and values chosen in a sample can be chosen again in future samples. This is performed *n* times, and the average of the *n* VARs computed is used.

## Non-Parametric VAR Estimation
*LO 2b: Describe historical simulation using non-parametric density estimation*

Historical simulation relies on observed data points. In this context, this implies that we have a limit number of observances to point to when performing analysis. If we have 50 data points and want to determine the 99th percentile VAR, we do not have a 49.5th data point to refer to. Non-Parametric Density Estimation resolves this issue by interpolating between observed data points.  

## Historical VAR Simulation Approaches
*LO 2c: Compare and contrast the age-weighted, the volatility-weighted, the correlation-weighted and the filtered historical simulation approaches*

### Age-Weighted Historical VAR Simulation
An issue with Historical VAR is the concept that...why are all data points in the data set equally relevant? Why is the 95th data point important but the 96th is not, for example. Age-Weighting solves this issue, albeit in a simplistic way, by gradually reducing the weight of data points as we step back in time.

$$w(i) = \frac{\lambda^{i-1}(1-\lambda)}{1-\lambda^n}$$

Where $\lambda$ is the decay factor, and $0<=\lambda<=1$. For example, w(1) would be $\lambda$ and w(2) would be $\lambda^2$. 

### Volatility-Weighted Historical VAR Simulation
This method weights values either up or down based on the volatility at the time (via GARCH or EWMA). This serves to account for time-varying volatility characteristics, to ensure that our VAR is not under or overestimated. 

$$r_{t,i} = \left ( \frac{\sigma_{T,i}}{\sigma_{t,i}} \right )r_{t,i}$$

Where...
* $r_{t,i}$ = the actual return for asset i on day t
* $\sigma_{t,i}$ = volatility forecast for asset i on day t (made at the end of day t-1)
* $\sigma_{T,i}$ = current forecast of volatility for asset i

For example, if volatility is currently 1 and was 0.5 on the day of the observation, we will multiply the value from that particular day by 2 (1/0.5). This allows for VAR estimates which are higher than the vanilla Historical Method.

### Correlation-Weighted Historical VAR Simulation
Correlation (or variance-covariance) weighting is similar to Volatility weighting but applied to the correlation between assets in a portfolio.

### Filtered Historical VAR Simulation
This is a comprehensive approach in which - for each data point - conditional volatility models are applied, and standardisation is performed by dividing the datapoint by realised returns. Bootstrapping is used to simulate returns which incorporate current volatility levels.

# Non-Parametric VAR Estimation: Advantages & Disadvantages
*LO 2d: Identify advantages and disadvantages of non-parametric estimation methods*

The advantages are that non-parametric methods are simple, flexible and avoid complicated variance-covariance matrices and the likes. Furthermore, we can apply time, volatility, and correlation-based weighting regimes to existing data with relative ease. 

The disadvantages, however, are that non-parametric methods are highly dependant on data. Therefore if data exhibits characteristics which are either too high or too low, then our estimates will be misleading. Non-parametric methods will not be able to detect regime changes, and of course, if an instrument is new, we won't have any historical data to use at all.

__References__

*Kevin Dowd, Measuring Market Risk, 2nd Edition (West Sussex, UK: John Wiley & Sons, 2005). Chapter 4. Non-parametric Approaches*
