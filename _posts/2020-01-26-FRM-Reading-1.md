---
title: "Estimating Market Risk Measures: An Introduction and Overview"
layout: post
---
Estimating Returns; VAR Method, Expected Shortfall & Coherent Risk Measures.

# Estimating Returns
Generally, this is...$P/L_t = P_t + D_t - P_t-1$...and we will have to be mindful that interim payments (e.g. dividends) might not necessarily be reflected in the price of the security. 

**Arithmetic Return Data:** We should use this when the interim payments are not reinvested. We usually would not use this for long periods, as one would assume reinvestment for such periods.

$$r_t =  \frac{P_t + D_t - P_{t-1}}{P_{t-1}} = \frac{P_t + D_t}{P_{t-1}} - 1$$

**Geometric Return Data:** We should use this to account for interim payment reinvestment. Lognormal returns are used to ensure that an asset's price can never be negative, so it can be used for 1) Long periods or 2) instruments which cannot have a value less than zero.

$$R_t =  ln*\frac{P_t + D_t}{P_{t-1}}$$

# Historical VAR Estimation
*LO 1a: Estimate VaR using a historical simulation approach*

Take all returns, order them by size. Historical VAR is the process of identifying the data point which separates the body of the distribution from the tail. The observation that determines VAR for *n* observations at the (1-a) confidence level would be (a * n) + 1.

**Note**: Confidence Levels are the big values (e.g. 95%) whereas the significant levels are the smaller levels (e.g. 5%). 

**Example** Identify the ordered observation in a sample of 1000 data points that correspond to VAR at a 95% confidence level (5% significance level). 

We're looking for the data point which separates the 95% of the 1000 data points from the 5% of the data points. The tail is (a * n) + 1. So we do (0.05 * 1000) + 1 = 51. 51 is the data point we use as the Historical VAR for this calculation.

**Note**: Be prepared to use both (a * n) + 1, as well as (a * n) for historical VAR.

If you are told that historical returns follow a normal distribution, then you can look at the z-table for this. Historical VAR approaches are only sensible when 1) we expect future return distributions to remain similar to historical return distributions and 2) unchanging parameter values.

# Parametric VAR Estimation
*LO 1b: Estimate VaR using a parametric approach for both normal and lognormal return distributions*

Parametric VAR estimation methods make specific assumptions about the underlying distribution of returns for an instrument. Two cases are mentioned which are 1) VAR for returns which follow a normal distribution and 2) VAR for returns which follow a lognormal distribution.

## Normal VAR

$$VAR(\alpha\%) = - \mu_{P/L} + \sigma_{P/L} * z_ \alpha$$

Where μ and σ are the mean and standard deviation of the P&L distribution and z denotes the critical value of the standard normal distribution. In most cases, we won't know what the population μ and σ are, so we will likely use sample values.

**VAR with Arithmetic Returns**
If you have arithmetic returns, such as a mean return of 10% with a standard deviation of 20%, you adjust this by multiplying the VAR result by the Portfolio Value. 

$$VAR(\alpha\%) = (- \mu_{P/L} + \sigma_{P/L} * z_ \alpha) * P_{t-1}$$

## Lognormal VAR

$$VAR(\alpha\%) = P_{t-1}  \times (1-e^{\mu_{R}-\sigma_{R} * z_ \alpha})$$

Lognormal VAR takes into account the concept of continuous-time returns, and/or continuously reinvested returns. The Lognormal distribution is right skewed - has a lot of positive outliers, and is bounded on the left by zero. 

# Risk Measures

## Expected Shortfall
*LO 1c: Estimate the expected shortfall given profit and loss (P/L) or return data*

Expected Shortfall is the average of the VAR in the tail mass of a VAR Calculation. For example, if the 5% VAR is $100, then the Expected Shortfall is the average of the 96, 97, 98 and 99 Confidence Level VARs. 

## Coherent Risk Measures
*LO 1d: Define coherent risk measures*

This is where we take the entire return distribution and create a weighted average of VAR for several slices of the distribution. For example, if *n* is 10, then we split the distribution into *n-1* slices, and assign each slice a risk aversion level. 

## Risk Measures & Quantiles
*LO 1e: Estimate risk measures by estimating quantiles*

Estimating a loss quantile involves mapping or plotting the frequency of losses on a distribution and separating them in terms of quantiles. This can be done on a percentage basis (e.g. the 90th %ile loss) or on a range basis, by identifying a "slice" of the distribution and determining a weighted average loss within that "slice".

## The Standard Error of a Risk Measure
*LO 1f: Evaluate estimators of risk measures by estimating their standard errors*

Estimators, depending on how they are created and how they are calculated, have different levels of precision. An estimator which is highly imprecise and has a wide margin of error (or standard error) is not going to be hugely useful in all cases. In this context, it is useful to evaluate its standard error by calculating...

$$[q+se(q)\times z_\alpha] > VAR > [q-se(q)\times z_{alpha}]$$

Where...
* $\alpha$ is the significance level
* $q$ is the quantile
* $se(q) = \frac{\sqrt{p(1-p)/n}}{f(q)}$

## Quantile-Quantile Plots (QQ Plots)
*LO 1g: Interpret quantile-quantile (QQ) plots to identify the characteristics of a distribution*

Quantile-Quantile (QQ) Plots are a way of identifying if empirical data matches a theoretical distribution (e.g. the Normal Distribution). Taking an example of comparing an empirical t-distribution vs. a normal distribution, we will see that within the 95% confidence level, the t-stats will match quite closely, but as the t-distribution has wider tails than the normal distribution, the t-stats at the 96%+ level will differ quite a lot.
