---
title: "VAR Model Backtesting"
layout: post
---
VAR Model Validation with Expected Failure Rates using Unconditional and Conditional Coverage models.

# VAR Backtesting
VAR backtesting is the process of analysing VAR model expectations versus realised returns. The comparison of the VAR model should be performed against *cleaned* returns, which are returns data which have been adjusted to remove effects which are not marked to market, such as funding costs, taxes, and so on.

## Failure Rates
Losses which exceed the VAR value at a given confidence level are referred to as *exceptions*. We expect to observe several exception data points in proportion to the confidence level; the implication being that too many or too few exceptions imply model misspecification. The *failure rate* is the number of exceptions as a proportion of the number of samples. The probability of an exception, *p*, is 1 - Confidence Level. *N* represents the number of exceptions; *T* represents the sample size. The failure rate is, therefore, *N/T* If the probability of an exception approaches and remains near the confidence level as the sample size increases, then we can consider the failure rate to be an unbiased measure. 

We can use this failure rate to test if a model is correctly specified by using a z-score calculation. In this context, the z-score calculation takes the form of...

$$z = \frac{x-pT}{\sqrt{p(1-p)T}}$$

In words, the z-score is equal to...

$$z = \frac{Exceptions-Probability(SampleSize)}{\sqrt{Probability(1-Probability)SampleSize}}$$

If the z-score is bigger than the critical value at the confidence level (e.g. 1.96 for 95%) then we can consider the failure rate to be biased. In more appropriate parlance, we would reject the null hypothesis that the model is unbiased. Hypothesis testing in this manner leads us neatly into our next topic.

## Type I & II Errors
When testing the validity of a model such as described in the previous section, we have the chance of either rejecting a model which is valid or accepting a model which is invalid. These are Type I and Type II errors respectively. We must design a validity test which has a reasonable trade-off between the Type I and Type II errors. 

## VAR for Potential Losses
When using VAR to communicate or measure potential losses, we must choose a sensible position holding period. An annual VAR for a firm which trades in minute-long time horizons would be incongruent. Therefore we should either use a VAR horizon which matches either...
1. The expected time required to liquidate the portfolio
2. The expected period in which risk-taking/mitigation activity will not occur

## The BASEL Committee's VAR Backtesting Rules
The BASEL committee will penalise banks if their VAR models exhibit model misspecification. An example of such a violation would be excessive exception occurences for a 95% confidence level VAR model employed by a bank. The BASEL committee specifies a table split into three sections - the Green, Yellow and Red sections - which characterise the bank's models based on exception occurrences. In the Yellow zone - which is between 5 to 9 exceptions - several criteria are used by BASEL supervisors to determine the penalty rate to be applied to the bank. Those criteria include...

1. Penalty Applied: The Basic Integrity of the Model
2. Penalty Applied: Model Accuracy
3. Penalty Considered: Intraday Trading Activity
4. Entirely Discretionary: Luck

# Coverage Models
Log-Likelihood ratios as used to determine model validity using tail values.

## Unconditional Coverage
The unconditional coverage model is used to estimate a measure used to accept or reject a model. The term "unconditional" refers to the fact that the data points in the model are unrelated or unconditional to each other. The time-varying occurrence of VAR exceptions is not taken into account, so not serial-correlation is considered. The model uses a log-likelihood ratio (LR) and is defined as follows:

$$LR_{uc} = -2ln\lbrace(1-p)^{T-N}p^N\rbrace+2LN\lbrace[1-(N/T)]^{T-N}(N/T)^N\rbrace$$

Where...
 * *$p$* = Probability Level
 * *$T$* = Sample Size
 * *$N$* = Number of Exceptions
 * *$LR_uc$* = Test Statistic for Unconditional Coverage (uc)

The key value to remember when dealing with the $LR_{uc}$ is that we reject the hypothesis that the model is unbiased if the value is > 3.84. The issue with using a high confidence level (conversely a low probability-of-exception level) is that at these levels, such as the 99% level, few exceptions occur, meaning that the user will sometimes struggle to determine a model is biased or whether it is simply subject to relatively few exceptions. For this reason, often 95% confidence levels are used. 

## Conditional Coverage
Extending the Unconditional Coverage model; Conditional Coverage, noted as $LR_{cc}$, accounts for time-varying clustering of VAR exceptions and thus implied serial-dependency. At a high level the Conditional Coverage model is given as...

$$LR_{cc} = LR_{uc} + LR_{ind}$$

At a 95% confidence level, we'll reject the unbiasedness of the model if $LR_{cc} > 5.99$, and we would reject the concept the indepdence of exceptions alone if $LR_{ind} > 3.84$
