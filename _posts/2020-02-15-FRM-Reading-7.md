---
title: "Correlation Basics: Definitions, Applications, and Terminology"
layout: post
---
We examine the role that correlation plays in financial markets, using examples from products including Credit Default Swaps (CDS), collateralised debt obligations (CDOs) and multi-asset correlation options. 

# Financial Correlation Risk
*Describe financial correlation risk and the areas in which it appears in finance.*

Correlation risk measures the risk of losses arising from changes in correlations between assets. Correlations between assets - both financial and non-financial - can be either Static or Dynamic. Static correlations remain fixed whereas Dynamic correlations are time-varying. 

Correlation can present problems when measuring the risk of various financial assets. Credit Default Swaps (CDS), for example, can potentially exhibit *Wrong Way Risk* if the reference object and the issuer exhibit positive default correlation to each other. A further complication is that the spread between a CDS and the object it references can be *nonmonotonous*, meaning that the spread changes over time given changes in correlation. 

## Correlations in Financial Investments
The standard deviation of a portfolio is determined by the variances of each asset, the position size weights of the asset, and the covariance between each asset. For a two-position portfolio, the portfolio standard deviation is...

$$\sigma_p = \sqrt{W^{2}_{X}\sigma^{2}_{X}+W^{2}_{Y}\sigma^{2}_{Y}+W_{X}W_{Y}COV_{XY}}$$

As a refresher, the Variance of an asset X is $(X_t - \mu_t)^2$ and the covariance of asset X and Y is $(X_t - \mu_X) \times (Y_t - \mu_Y)$.

## Correlation in Trading with Multi-Asset Options
There are various assets which can be traded, whose values are determined by the correlation between assets. The following is a summary of the payoff profile of some of thse assets...

| Correlation Strategies               | Payoff                                     |
|--------------------------------------+--------------------------------------------|
| Option on higher of two stocks       | $max(S_1,S_2)$                             |
| Call option on the max of two stocks | $max[0, max(S_1, S_2)-K]$                  |
| Exchange option                      | $max(0, S_2 - S_1)$                        |
| Spread call option                   | $max(0, S_2 - S_1$ - K)                    |
| Dual-strike call option              | $max(0, S_1 - K_1, S_2 - K_2)$             |
| Portfolio of Basket Option           | $max[\sum^{n}_{i=1}n_i \times S_i - K, 0]$ |

# Correlation Risk Management, Correlation Swaps, and the 2007/8 Financial Crisis

## Risk Management
*Estimate the impact of different correlations between assets in the trading book on the VaR capital charge.*

The formula for calculating VAR using the variance-covariance method is...

$$VAR_p = \sigma_p\alpha\sqrt{x}$$

Where...
* $\sigma_p$ is portfolio daily volatility
* $\alpha$ is the z value from the standard normal distribution (or the significance level)
* $x$ is the number of trading days

Within $\sigma_p$ the correlation of assets in the portfolio is defined as...

$$\sigma_p = \sqrt{\beta_h\times C \times\beta_v}$$

Where...
* $\beta_h$ is the horizontal beta vector
* $C$ is the coraviance matrix of returns
* $\beta_v$ is the vertical beta vector

Computing portfolio VAR using the variance-covariance method by hand is burdensome, but not impossible. An example is provided below. 

*Example Portfolio VAR Calculation*

Assume we have a two-asset portfolio with positions of 8m in Asset A, 4m in Asset B, a correlation coefficient of 0.6 with daily standard deviations of 1.5% and 2% for Assets A and B respectively. What is the 10-Day VAR at the 99% confidence level for this portfolio?

In order to apply our $VAR_p = \sigma_p\alpha\sqrt{x}$ formula, we need the $\sigma_p$ parameter, which is dependant on a covariance matrix.

$$\begin{pmatrix}
cov_{11} & cov_{12} \\ 
cov_{21} & cov_{22}
\end{pmatrix}
= 
\begin{pmatrix}
\sigma^{2}_{1} & \rho_{12}\times\sigma_1\times\sigma_2 \\ 
\rho_{12}\times\sigma_1\times\sigma_2 & \sigma^{2}_{2}
\end{pmatrix}$$

$$\begin{pmatrix}
0.015^2 & 0.6\times0.015\times0.02 \\ 
0.6\times0.015\times0.02 & 0.02^2
\end{pmatrix}
= 
\begin{pmatrix}
0.000225 & 0.00018 \\ 
0.00018 & 0.0004
\end{pmatrix}$$

This process gives us the covariance matrix. We will now use the formula $\sigma_p = \sqrt{\beta_h\times C \times\beta_v}$ as mentioned before. 

*Step 1: Multiply the Horizontal Beta Vector by the covariance matrix*

$$\beta_h * C= [8\,\,4] * \begin{pmatrix}0.000225 & 0.00018\\0.00018 & 0.0004 \end{pmatrix}$$

$$= [(8\times0.000225)+(4\times0.00018)\,\,\,(8\times0.00018)+(4\times0.0004)]$$

$$=[0.00252\,\,\,0.00304]$$

*Step 2: Multiply the Vertical Beta Vector by the results of Step 1*

$$(\beta_h\times C)\times\beta_v$$

$$= [0.00252\,\,\,0.00304]\begin{bmatrix} 8\\4\end{bmatrix}$$

$$= (0.00252\times8)+(0.00304\times4) = 0.03232$$

*Step 3: Compute $\sigma_p$ by square-rooting the result*

$$\sigma_p = \sqrt{(\beta_h\times C)\times\beta_v} = \sqrt{0.03232} = 0.01798 \,or\, 17.98\%$$

*Step 4: Compute the original formula for Portfolio VAR*

$$VAR_p = \sigma_p\alpha\sqrt{x} = 0.1798\times2.33\times\sqrt{10} = 1.3248$$

The value is in terms of $USD millions. Note the BASEL committe requires banks to hold at least three times their 10-Day VAR to finance the trading book. 

## Correlation Swaps
*Describe the structure, uses and payoffs of a correlation swap.*

It is possible to purchase or sell correlation risk, or time-varying correlation, via the use of Correlation Swaps. The payoff of these swaps for a buyer is $notional\,amount \times (\rho_{realised}-\rho_{fixed})$, where...

$$\rho_{realised} = \frac{2}{n^2-n}\sum_{i>j}\rho_{i,j}$$
