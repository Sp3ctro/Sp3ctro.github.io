---
title: "Correlation Modelling - Bottom-Up Approaches"
layout: post
---
Copulas and their use in modelling correlations for non-normally distributed variables. 

# Copula Terminology
Before we discuss copulas, their forms, and how they can be used to model correlations, it is best to make some informal definitions clear...

**Univariate Distribution**
A univariate distributon is the probability distribution of a single variable, or single number. Such distributions include the Normal, Student's T, Chi-Squared, F, Exponential, and Gamma distributions

**Marginal Distribution**
A marginal distribution is the probability distribution of a sample set taken from another distribution. For example, if you have a vector of 100 observances; plotting the distributon of a sample of 20 of those observances is a marginal distribution. 

**Multivariate Distribution**
A multivariate distribution is a combination of 2 or more variables, such that a linear combination of those variables fits a distribution. For example the Standard Normal Multivariate Distribution is a vector of multiple normally distribted variables, such that any linear combination is also normally distributed.

**Joint Cumulative Distribution**
A joint cumulative distribution function is a two-dimention cumulative distribution function. 

**Inverse Functions**
An inverse function is usually the inverted form of a probability distribution. 

**Copula**
A copula is a combination of two or more marginal distributions. Specifically it is a function which identifies how the values from two distributions "join together". Copulas are particularly useful at identifying the correlation between two variables which have non-normal distributions. 

**Gaussian Copula**
A Gaussian Copula is the "normal distribution" equivalent of a copula.

# Correlation Copulas
A copula function can transform an n-dimensional function to a univariate function $C:[0,1]^n\rarrow[0,1]$. 

$$C[G_1(u_1),...,G_n(u_n)] = F_n[F_n^-1(G_1(u_1)),...,F_n^-1(G_n(u_n));\rho_F]$$

Where...
$G_i(u_i)$ are the marginal distributions
$F_n$ is the joint probability distribution
$F_1^-1$ is the inverse function of $F_n$
$\rho_F$ is the correlation matrix structure of the joint cumulative function F_n

**Note** if you only have two marginal distributions, you do not need to include a correlation matrix as part of $\rho_F$, you only need a single correlation term. 

## Gaussian Copulas
Gaussian copulas map marginal distributions - which have unknown properties - to the normal distribution. This is done by mapping values from one distribution to the other on a percentile basis. This is often used in Finance to create Gaussian Default Time copulas.
