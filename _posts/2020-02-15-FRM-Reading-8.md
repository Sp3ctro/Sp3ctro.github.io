---
title: "Empirical Properties of Correlation"
layout: post
---
Real life properties of Correlation.

# Correlations During Different Economic States
*Describe how equity correlations and correlation volatilities behave throughout various economic states.*

At a high level, equity correlations are highest in times of recessions and lowest in times of economic expansions. equity correlation volatility, however, is highest in normal market conditions, as there is uncertainty around which direction the economy will go. In other words; equity correlation gamma is high.

## Mean Reversion & Autocorrelation
*Calculate a mean reversion rate using standard regression and calculate the corresponding autocorrelation.*

Mean reversion is statistically defined as...

$$\frac{\delta(S_t - S_{t-1})}{\delta(S_t-1)}$$

The rate at which a variable returns to its long-run mean is defined as mean reversion speed...

$$S_t - S_{t-1} = a(\mu - S_{t-1})\Delta t + \sigma_S\epsilon\sqrt{\delta t}$$

We can simplify this by removing $\sigma_S\epsilon\sqrt{\Delta t}$ and assuming that $\Delta t$ is 1...

$$S_t - S_{t-1} = a(\mu - S_{t-1})$$

We can determine mean reversion rate by running a standard regression in which we transform $S_t - S_{t-1} = a(\mu - S_{t-1})$ into a usual regression equation:

$$S_t - S_{t-1} = Y; a\mu - \alpha; -aS_{t-1} = \beta X$$

The beta coefficient here is the negative of the mean reversion rate. -0.78 for example means 78% mean reversion. 

*Autocorrelation* measures the correlation coefficient of a variable to its previous variable. Autocorrelation can be thought of as the opposite of mean-version, where autocorrelation identifies tendencies for values to be pulled towards the most recent observations. 

*Note* the Autocorrelation rate is = 1-Mean Reversion Rate

Autocorrelation for a 1-period lag is...

$$AC(\rho_t, \rho_{t-1}) = \frac{cov(\rho_t, \rho_{t-1})}{\sigma(\rho_t)\times(\sigma_{t-1})}$$

## Best Fit Distributions for Correlation Modelling
*Identify the best-fit distribution for equity, bond and default correlations*

Empirical studies[^1] performed on equity, bond and default correlations during normal market conditions and times of stress will produce different results depending on the distribution used. Furthermore, the robustness of these models will differ depending on the quality of fit of each distribution. The best fit and most robust distribution for Equity and Default Correlations is the Johnson SB distribution. The Generalised Extreme Value (GEV) distribution is best-fit for Bond correlations, but researchers note that the Normal distribution is also usable.

[^1] Meissner, G. (2014). Correlation risk modeling and management. Singapore: John Wiley & Sons.
