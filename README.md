# econ3916-lab12-ols-prediction
# OLS as a Line of Best Fit: Estimation versus Prediction

## Objective
I used the California Housing data (20,640 districts) to see how the same least-squares machinery answers two different questions — what a coefficient is, and how well a model predicts districts it has not seen.

## Methodology
- I regressed median house value on median income three ways: the closed-form slope formula (covariance over variance), statsmodels, and scikit-learn, and checked that all three gave the same intercept and slope.
- I added 0, 1, 5, 20 and 100 columns of random noise beside median income and recorded R-squared and adjusted R-squared each time.
- I split the data into training rows (80%) and test rows (20%) before fitting anything, then fitted an eight-feature model on the training rows and scored it on both sets.
- I used one specification, value on median income and rooms per household, for two jobs: reading the AveRooms coefficient and its 95% interval, and measuring the test RMSE.
- I wrote a function, `holdout_rmse()`, that takes a table and a list of predictors, splits the data the same way every time, fits on the training rows and returns the test RMSE. I used it to score median income on its own.

## Key Findings
- All three methods gave the same slope, 0.417938.
- R-squared rose from 0.4734 with no noise to 0.4758 with 100 noise columns, even though the noise has nothing to do with house value. Adjusted R-squared did not keep rising.
- The eight-feature model had a train RMSE of 0.7197 and a test RMSE of 0.7456 (value is in $100,000s). The test error is the honest measure of how the model does on new districts.
- Holding income fixed, the AveRooms coefficient was −0.0381, with a 95% CI of [−0.0430, −0.0333]. That is a precise estimate, but the same two-predictor model predicted worse than the eight-feature one.
- With median income alone, the test RMSE was 0.8421, compared with 0.7456 for all eight features. Because both were scored on the same test rows, this is a fair comparison, which in-sample R-squared is not.
