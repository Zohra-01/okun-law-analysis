# Plan: Does Okun's Law Still Hold?

## Question and Expectation

Does Okun's law still hold over the last 20 years? I expect a negative coefficient of about -0.4 to -0.5 when I regress the quarterly change in the unemployment rate on real GDP growth. When the economy grows, firms demand more labor and unemployment falls. When it shrinks, firms cut jobs and unemployment rises. The 2008 recession and COVID-19 are the two biggest tests. I expect them to add noise, since unemployment moved much more than GDP predicted in 2020, but I do not expect them to change the sign.

## Data Sources

- Unemployment rate: FRED series UNRATE (monthly, percent).
- Real GDP: FRED series GDPC1 (quarterly, billions of chained 2017 dollars).
- Package: fredapi, with the API key stored in a .env file.

## Cleaning Steps

- Date range: 2005 to 2025 (last 20 years).
- Align frequency: take the quarterly average of monthly UNRATE, which is the standard approach. In pandas this is resample("QS").mean(), which gives one value per quarter.
- Merge: join the two series on the quarter start date.
- Missing values: check for gaps after the merge and drop or flag them.
- Transformations: unemployment change (first difference of the quarterly rate) and GDP growth (percent change in real GDP).

## Charts and Tests

- Charts: line chart of both series over time, and a scatter plot with a fitted regression line.
- Test: OLS regression with statsmodels, reporting the coefficient, its p-value, and R-squared.

## What Would Support or Contradict My Expectation

- Support: a negative and statistically significant coefficient near -0.4 to -0.5.
- Contradict: a coefficient near zero, positive, or not statistically significant.