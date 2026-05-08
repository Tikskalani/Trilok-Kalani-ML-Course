# Lab 11 — Hyperparameter Tuning and AutoML

This lab was about squeezing more performance out of a model after you've picked it. Two angles: tune the hyperparameters yourself, or hand the whole problem to an AutoML library and see how it does.

## File

- `L11_Trilok_ITAI1371.ipynb`

## What I did

**Manual tuning with GridSearchCV.** Took a Random Forest classifier on the Iris dataset and ran a grid search over `n_estimators`, `max_depth`, and `min_samples_split`. The grid search trains a model for every combo and picks the best one based on cross-validated accuracy.

**Random search.** Ran the same kind of thing using `RandomizedSearchCV`, which samples random combinations from a distribution instead of trying every grid point. Faster, and usually within striking distance of the grid's best.

**AutoML with AutoGluon.** Loaded `TabularPredictor`, gave it the same training data, and let it do its thing. It trained a stack of models (linear models, tree models, neural nets, ensembles) and picked the best one automatically.

## Takeaways

Grid search is exhaustive but it gets expensive fast. With three hyperparameters at five values each, that's 125 model fits, times 5 cross-validation folds — already 625 fits before you've really tuned anything. Random search hits 80% of the gain in 20% of the time on most problems.

AutoML is genuinely impressive on a tabular problem. AutoGluon basically gave me a stronger model than I would have built by hand on this dataset, in less time. The catch is that you give up understanding — when AutoGluon hands you back a stacked ensemble, you don't really know which features it cares about or why. For coursework it's fine. For something you'd ship to production, you probably want the interpretability.

Used GridSearchCV again in the final project on HistGradientBoosting and got my best regression model from it (R² 0.42).
