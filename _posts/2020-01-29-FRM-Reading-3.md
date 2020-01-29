---
title: "Parametric VAR Estimation: Part 2"
layout: post
---
Modelling extreme outliers resulting from catastrophic and Black Swan-like events, using Generalised Extreme Value (GEV) distributions, and the Peaks-Over-Threshold approach.

# Extreme Values

Extreme values are rare; they manifest as a result of major market declines, collapses of systematically important entities, or significant macroeconomic events. By definition, empirical data about these events are scarce. Distributions - which have an expected degree of error - are used to model these events.

## Fisher-Tippett Theorem
The Fisher-Tippett Theorem suggests that as a sample set of *n* data points gets large, the distribution of extreme values, denoted by $M_n$, converges to the Generalised Extreme Value (GEV) Distribution.

$$F(X \mid  \xi, \mu, \sigma) = exp\left [-\left ( 1+\xi\times\frac{x-\mu}{\sigma} \right )^{-1/\xi} \right ] if \xi \neq 0$$

$$F(X\mid\xi, \mu, \sigma) = exp\left [ -exp\left ( \frac{x-\mu}{\sigma} \right ) \right ] if \xi = 0$$

With the restriction of...

$$\left ( 1+\xi\times\frac{x-\mu}{\sigma} \right )>0$$

Where...
* $\mu$ is the location parameter
* $\sigma$ is the scale parameter

If $\xi > 0$ then the GEV becomes a Frechet distribution. If $\xi = 0$ then the GEV becomes a Gumbel distibution. If $\xi < 0$ then the GEV becomes a Weibull distribution. The final case does not occur often in Financial Markets. When choosing whether to model a Frechet or Gumbel distribution we must consider the following pieces of information...

1. If we're confident in the distribution, then we should assume that $\xi > 0$
2. If we cannot reject the null hypothesis that $\xi = 0$ then we should assume that $\xi = 0$
3. If we're otherwise unsure we should probably use $\xi > 0$

## Peaks-Over-Threshold
Peaks-Over-Threshold models the minima and maxima of a large sample. It defines a random variable *X* as being the loss, and defines *u* as being the threshold value for positive values of $x$. The distribution of excess losses over our threshold *u* is:

$$F_u(x) = P \\{ X - u \leq x \mid X > u \\} = \frac{F(x+u)-F(u)}{1-F(u)}$$

## Generalised Pareto Distributions

The Gnedenko-Pickands-Balkema-deHaan (GPBdH) theorem says that as *u* gets large, the distribution $F_u(X)$ converges to the generalised Pareto (GP) distribution, such that...

$$1 - \left [ 1+\frac{\xi }{\beta} \right ]^{-1/\xi} if \xi \neq 0$$

$$1 - exp \left [ -\frac{x}{\beta} \right ] if \xi = 0$$

The GP distribution dips below the normal distribution just before the tails, but then moves above the normal distribution around the extreme tails. 

## VAR and Expected Shortfall

The POT approach serves to add to the VAR estimation process, in which we can provide not only a VAR value, but also the expected shortfall when the VAR is exceeded (or in numerical terms; $E\left [ L_p \mid L_p > VAR \right ]$). 

VAR with POT parameters is...

$$VAR = u + \frac{\beta}{\xi}\left \\{ \left [ \frac{n}{N_u}(1- Confidence Level) \right ]^{-\xi}-1 \right \\}$$

Where...
* $u$ = threshold (in percentage)
* $n$ = number of observations
* $N_u$ = number of observations that exceed the threshold

and Expected Shortfall is...

$ES = \frac{VAR}{1-\xi}+\frac{\beta-\xi u}{1-\xi}$

### Example - Compute VAR and ES given POT Parameters

Given...
* $\beta$ = 0.75
* $\xi$ = 0.25
* $u$ = 1%
* $N_u/n$ = 5%

Compute the 1% VAR in percentage terms and the corresponding expected shortfall measure.

$VAR = 1+\frac{0.75}{0.25}\left \{ \left [ \frac{1}{0.05}(1-0.99) \right ]^{-0.25}-1 \right \} = 2.486\%$

$ES = \frac{2.486}{1-0.25} + \frac{0.75 - 0.25\times1}{1-0.25} = 3.981\%$

## Comparing Generalised Extreme Value & Peaks-Over-Threshold Methods

GEV focuses on the distribution of extreme values, whereas Peaks-Over-Threshold focuses on the distribution of values in excess a certain high mark threshold. GEV requires more data than POT; however the POT approach requires us to pick a certain threshold to use, so there are trade-offs to both.

## Multivariate Extreme Value Theory

Multivariate EVT focuses on tail dependance, such as when a major decline in one market can lead to a major decline in some related market. Multivariate EVT will use Extreme Value Copulas; a Copula being a combination of univariate distributions forming a new "combined" distribution. The observations which occur in a Multivariate EVT Copula decrease in frequency as we add more dimensions to the copula. E.g. if we have 2 dimensions each with a EV of 1 in 100 times, we'll only see an EV in the combined distribution 1 in 100 * 100 = 10,000 times.  
