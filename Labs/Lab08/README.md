# Lab 08 — The Bias-Variance Tradeoff

This lab was about *seeing* overfitting and underfitting instead of just reading about them. The exercise was to fit polynomial regressions of different degrees and watch what happens to the training and test errors as model complexity goes up.

## File

- `L08_Trilok_ITAI1371.ipynb`

## What I did

Generated some noisy synthetic data and then fit polynomial regressions of degree 1, 2, 5, and 15 using `make_pipeline` with `PolynomialFeatures` and `LinearRegression`. Then I plotted each fit on top of the data and made a learning curve using `learning_curve`.

## What it actually looked like

- Degree 1: clearly underfitting. The straight line missed the shape of the data.
- Degree 2 / 3: visually a good fit. Training and test errors were close.
- Degree 15: training error practically zero, test error blew up. The model was passing through almost every training point but the curve between them was wild.

That last picture is what overfitting actually looks like. I'd seen the words a hundred times but watching the curve wiggle through every training point while completely missing where the next test point would land made it real.

## The takeaway

The bias-variance tradeoff isn't a thing you fix once, it's a knob you have to keep adjusting. More complexity reduces bias but increases variance. Less complexity does the opposite. Cross-validation is how you figure out where the sweet spot is for a given dataset.

This idea came back during the final project, where ridge regression beat plain linear regression on the audio-only feature set, and tuning HistGradientBoosting's `max_iter` and `learning_rate` was basically a fight against this same tradeoff.
