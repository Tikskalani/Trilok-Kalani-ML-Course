# Lab 06 — Linear and Logistic Regression

This is where we built the first "real" models from scratch. Linear regression for a continuous target, logistic regression for a binary one. The lab walked through both halves end to end.

## File

- `L06_Trilok_ITAI1371.ipynb`

## Part 1 — Linear Regression

I generated a synthetic dataset using `make_regression`, split it into train and test sets, fit a `LinearRegression` model, and evaluated it with mean squared error. Then I plotted the regression line over the data points to actually see the fit.

What clicked: the model is learning two numbers — a slope and an intercept — and that's it. It feels almost too simple, but it's the foundation everything else builds on.

## Part 2 — Logistic Regression

For the classification half I trained a Logistic Regression on a binary classification task and evaluated it with accuracy and a confusion matrix.

The thing that confused me at first was the name — "logistic regression" sounds like a regression algorithm, but it's actually classification. The "regression" part comes from the fact that it's learning weights for a linear combination of features; the trick is that it then squashes the output through a sigmoid to get a probability.

## Tools used

`sklearn.linear_model.LinearRegression`, `LogisticRegression`, `train_test_split`, `mean_squared_error`, `accuracy_score`, `confusion_matrix`

## Takeaways

- Linear models are surprisingly competitive when the relationship really is roughly linear, and they're fast and easy to interpret.
- They fall apart when the relationship is nonlinear. (My final project ended up being a great example of this — linear regression on Spotify audio features got R² = 0.03, basically nothing.)
- Always check the residuals, not just the score.
