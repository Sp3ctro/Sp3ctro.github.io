---
title: "Messages from the academic literature on risk measurement for the trading book"
layout: post
---
Notes & commentary from Academic Literature on VAR estimation. 

# VAR Estimation - Academic Comments
Although VAR estimation is widely used and easily calculated, some considerations must be taken into account when managing risk using VAR estimations.

## VAR Implementation
*Explain the following lessons on VaR implementation: time horizon over which VaR is estimated, the recognition of time varying volatility in VaR risk factors and VaR backtesting*

To start, there is no consensus on a best VAR timeframe, and therefore there is no accepted method for aggregating VAR estimations at different time horizons. The impacts from *time-varying volatility* reduces as the time horizon increases. However, we must adjust somehow for the effects of stochastic jumps, as well as the time-varying correlation between assets. The BASEL committee recommends a 10-day VAR time horizon. The usage of time horizons such as six months or 1 year might be necessary for economic capital planning purposes, but we should remember that such a time horizon may fail to adequately account for time-varying characteristics such as correlation and volatility, as well as the portfolio's composition over time. Generally, we use *model validation* to validate VAR models, however, this can be difficult or impossible if there are few exceptions available. 

## Liquidity Considerations
*Describe exogenous and endogenous liquidity risk and explain how they might be integrated into VaR models*

In times of market stress, the contraction of liquidity results in a change in the *liquidity horizon* of an investment. The effect is that the time required to unwind a position without materially impacting the market price of a security is increased. *Exogenous liquidity* is a market-specific adjustment to a VAR calculation to account for transaction costs. *Endogenous liquidity* is an instrument-specific adjustment to the VAR calculation to account for price impacts. As market stress is the catalyst for a "flight to quality", endogenous liquidity is of particular importance when estimating VAR for portfolios of thinly traded assets. 

# Risk Measures
*Compare VaR, expected shortfall and other relevant risk measures*

As discussed before, VAR estimates reveal the maximum loss at a specified confidence level, however, they do not describe the loss beyond this confidence level. For these purposes, we should use either *Expected Shortfall* or *Spectral risk measures* to evaluate the loss in the tails of the distribution.

# Stress Testing
*Compare VaR, expected shortfall and other relevant risk measures*

Stress testing is important to ensure that we capture the possibility and impacts of *historical scenarios, predefined scenarios, and mechanical-search scenarios*. Mechanical-search stress tests are a methodical process in which we stress various factor exposures in a portfolio. While stressing the correlation factor specifically, we must remember that correlation convergence will not happen instantaneously, and that portfolio managers will often have an opportunity to hedge on the onset of market stress.

## Integrated Risk Measurement
*Unified* approaches to risk management consider all risks at once. This can help in identifying compounding risk effects which might not be obvious when looking at risks on a standalone basis. Banks use a *compartmentalised risk management approach* to determine their capital; capital for different risk types - such as market and credit risk - are summed at the firm level. The BASEL framework uses a building block approach in which a bank's regulatory capital requirement is the sum of the capital requirements for various risk categories. Pillar 1 Risk includes market, credit and operational risk. Pillar 2 risk includes concentration risks, stress tests and other risks such as liquidity, residual, and business risks. In general, this approach is non-integrated, as risk factors are evaluated in isolation and summed at the firm level.

## Risk Aggregation
A firm's businesses are a set of portfolios which make up an overall entity-level umbrella. The *top-down* approach to risk aggregation assumes that a bank's risk can be properly separated into market, credit and liquidity risk factors. Academic studies evaluate the effectiveness of each approach by determining the ratio of unified to compartmentalised capital; essentially evaluating the risk diversification benefit. The ratio is less than one, which does imply that such diversification does exist. If a bank is not able to ringfence its risks, then the bank's capital level should be greater than the sum of the compartments it can successfully create.

# Balance Sheet Management
*Describe the relationship between leverage, market value of asset and VaR within an active balance sheet management framework*

Balance sheets tend to be procyclical, meaning that as prices rise, capital requirements will also rise. Leverage is counter-cyclical meaning that as prices rise leverage declines and vice-versa. Oftentimes target VAR levels are constrained by a bank's equity, and due to the previously mentioned procyclicality of balance sheet sizes, economic and price grown can increase risk-taking activity.  
