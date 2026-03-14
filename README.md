# Predicting the Proportion of Conservative Votes in a Canadian Federal Election

## Project Overview

This project estimates the proportion of Canadians likely to vote for the Conservative Party in a future federal election using survey data and demographic information. The analysis applies a logistic regression model combined with post-stratification to estimate voting behaviour across the Canadian population.

Using demographic predictors such as age and gender, the model estimates the probability that an individual supports the Conservative Party. These probabilities are then weighted using census demographic distributions to estimate the overall proportion of Conservative voters in the population.

The final estimate suggests that approximately 34.7% of the population would vote Conservative based on the modeled relationships between demographics and voting preferences.

## Dataset

### Canadian Election Study (2019)

The primary dataset used in this analysis comes from the 2019 Canadian Election Study, which surveys Canadian citizens on political attitudes, demographics, and voting preferences.

Key details:
- Data collected via phone and web surveys
- 4,021 respondents during the election period
- Survey responses include demographics and intended vote choice

### General Social Survey (2017)

Population demographic information was obtained from the General Social Survey, which provides census-style demographic distributions used for weighting the predictions.

The survey includes:
- Age
- Gender
- Province
- Population frequencies

These demographic distributions allow predictions from the regression model to be scaled to represent the national population.

## Data Preparation

Several cleaning steps were performed before modeling:
- Removed respondents who did not report a valid political party preference
- Filtered observations to include only male and female respondents to match census categories
- Removed respondents from territories not represented in the census data

Created new variables including:
- age (derived from birth year)
- support_conservative (binary indicator variable)
- cons_proportion (proportion of conservative supporters)

These steps ensured the survey data aligned with the demographic variables available in the census data.

## Exploratory Analysis

Exploratory summaries were used to understand how conservative political support varies across demographics.

Key relationships explored:

Gender: Male respondents showed a higher proportion of conservative support compared to female respondents.

Age: Conservative support tended to increase with age, with older age groups showing the highest proportions.

Province: Provincial differences in political support were observed, with larger provinces such as Ontario and British Columbia contributing the greatest share of conservative voters due to population size.

## Methods

### Logistic Regression Model

A logistic regression model was used to estimate the probability that an individual supports the Conservative Party.

The response variable:
support_conservative (1 = supports conservative, 0 = does not)

Predictor variables:
Age
Gender

The estimated model was:

𝑦 = − 1.4739 + 0.0107(age) + 0.5272 (male)
y=−1.4739+0.0107(age)+0.5272(male)

This model estimates the log-odds that a person supports the Conservative Party based on their demographics.

## Post-Stratification

Post-stratification was used to adjust predictions so they reflect the actual demographic distribution of the Canadian population.

Steps:
- Use the logistic regression model to predict the probability of voting Conservative for each individual in the census data.
- Group observations by province.
- Weight predictions by the population size of each demographic group.
- Aggregate weighted predictions across provinces.

This approach ensures the final estimate properly reflects the population composition rather than just the survey sample.

## Results

Using the weighted predictions, the estimated proportion of Conservative voters in the population was:

Estimated Conservative Vote Share:
0.347 (34.7%)

This value represents the predicted share of the population likely to vote Conservative given the demographic relationships observed in the survey data.

## Tools Used

- R
- tidyverse
- ggplot2
- survey package
- logistic regression modeling
