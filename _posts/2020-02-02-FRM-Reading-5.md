---
title: "VAR Mapping"
layout: post
---

Separating the risk of a multi-asset portfolio into distinct factor-based VARs, and the calculation of diversified, and undiversified VAR.

# What is VAR Mapping?
*Explain the principles underlying VaR mapping and describe the mapping process*

VAR mapping is the process of measuring the risk of a portfolio in terms of risk factors common to the - potentially quite varied - book of assets. VAR mapping can also help measure the risk of assets which have little historical data available regarding them, by transforming the asset-specific risk into a general measure of risk exposure. An example of this is measuring the risk of a bond in terms of generalised interest-rate risk. 

VAR mapping aggregates risk exposure which removes the need to measure & manage the risk of each position in the portfolio individually
1. VAR mapping expresses the portfolio's risk in terms of risk factors common to its positions
2. VAR mapping facilitates risk aggregation across instruments where aggregation using price-based methods might not be possible
3. VAR mapping is useful for measuring time-varying characteristics of portfolio risk
4. VAR mapping is useful when historical data about a position is not available      

## The VAR Mapping Process
*Explain how the mapping process captures general and specific risks*

The VAR mapping process involves reducing a portfolio of assets to a risk exposure expressed in terms of their *General Risk Factors*. Their *Specific Risk Factors* will be the individual position's idiocyncratic exposures; given we often deal with portfolios of dozens, hundreds or even thousands of positions with their idiosyncratic risks, we can consider maximum diversification and simply ignore these position-specific risks. 

For example, for Cash Equities, we can consider that a portfolio of 30 or more (or so) positions is sufficiently diversified, and that the idiosyncratic risk has been mostly mitigated. Each position in our portfolio will have an Equities Market Exposure of...

$$R_i = \alpha_i + \beta_i\,R_M+\epsilon_i$$

This is a regression of the position's returns given the return of the market. If the weight of each position in the portfolio is $w_i$ then the portfolio return can be defined as...

$$R_p = \sum_{i=I}^{N} \, w_i \, R_i = \sum_{i=I}^{N} \, w_i \, \beta_i \, R_m + \sum_{i=I}^{N} \, W_i \, \epsilon_i$$

The beta of the portfolio is...

$$\beta_p = \sum_{i=I}^{N} \, W_i \, \beta_i$$

We can decompose the variance of the portfolio into our two risk exposure components - general (market) and specific (idiosyncratic) risk as follows; if the variance of the portfolio is...

$$V(R_p) = \beta_{p}^{2}\,\times\,V(R_M)\,+\,\sum_{i=I}^{N}\,W_{i}^{2}\,\times\,\sigma^{2}_{\epsilon, i}$$

General Market Risk: $\beta_{P}^{2}\,\times\,V(R_M)$

Specific Risk: $\sum_{i=1}^{N}\,W_{i}^{2}\,\times\,\sigma_{\epsilon, i}^{2}$

## VAR Mapping for Fixed Income Securities
*Differentiate among the three methods of mapping portfolios of fixed income securities*

The three method of VAR mapping for fixed income securities are 1) principal mapping, 2) cash flow mapping and 3) duration mapping.

**Principal Mapping**
This method considers only the risk arising from the repayment of the bond's principal. We use the average maturity of the portfolio to find an equivalent zero-coupon bond, and use that as a proxy. This is the simplest approach.

**Cash Flow mapping**
The risk of each bond is decomposed into their respective cash flows. We use zero-coupon bonds as proxies for each cash flow and include inter-maturity correlations in the mapping process. 

**Duration Mapping**
The risk of the bond is mapped to a zero-coupon bond of the same duration. This is similar to the first approach, but using duration. 

## VAR Mapping for Linear Derivatives
*Summarize how to map a fixed income portfolio into positions of standard instruments*

Linear Derivatives are generally risk-mapped by decomposing their cash flows and payoff profiles into their risk-factors. This is similar to the process where we replicate the payoff of the instrument using borrowing/lending at the risk-free rate and purchasing a bond or equity as we do with Options for example. 

### VAR Mapping for Forward Contracts
Forward positions, such as a Long EURUSD Forward used in this example, can generally be decomposed into three separate risk positions...
1) A short position in the U.S. Treasury Bill, representing the risk-free rate
2) A long position in the One-Year Euro Bill
3) A long position in Spot Euro

These individual risk exposures can be used to compute the factor-based VAR.

### VAR Mapping for Forward Rate Agreements (FRAs)
Forward Rate Agreements can be decomposed into long & short interest rate exposures; DV01 and/or Duration can be used once this is done.

### VAR Mapping for Interest Rate Swaps
Taking a swap which pays a fixed rate in exchange for a floating rate, the steps required to compute the undiversified and diversified VARs are as follows: 

1) Calculate the PV of the short fixed-rate cash flows, and add the PV of a floating rate bond
2) For each cash flow, compute the VAR at the desired confidence level; the sum is the undiversified VAR
3) Using the variance-covariance matrix, calculate the diversified VAR

## VAR Mapping for Non-Linear Derivatives
Although Options have non-linear risk exposures, we can still use the delta-normal VAR approach to perform VAR mapping for short time-horizons. For example, assume the strike price of an option is $100 with a volatility of 25%. With a 1-day time horizon, we can compute the VAR as...

$$-\alpha S \sigma \sqrt{T}$$

...Where *T* is expressed in terms of 1 year; in this example, *T* is 1/252. 

# Stress Testing
*Describe how mapping of risk factors can support stress testing*

Stressing a portfolio VAR involves - among other things - assuming that the correlation among assets in the portfolio is 1. This effectively throws away any diversification benefits we get from holding more than one asset and assumes the worst-case scenario; that the VAR of the portfolio is the sum of the VAR of each position.

## Portfolio Benchmarking
*Explain how VaR can be used as a performance benchmark*

Portfolio benchmarking is the process of comparing the decomposed VAR of your portfolio to that of another portfolio.
