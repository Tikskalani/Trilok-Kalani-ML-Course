# Lab 05 — Data Preparation

Raw data is almost never ready for a model. This lab was about the preprocessing steps you have to do before training anything — and why each one matters.

## File

- `L05_Trilok_ITAI1371.ipynb`

## What the lab covered

- Handling missing values (drop vs. impute, and when each is appropriate)
- Scaling numeric features using `StandardScaler`
- Encoding categorical variables (label encoding vs. one-hot)
- Feature engineering — creating new columns from existing ones

## What I learned

The biggest "aha" was scaling. Linear and distance-based models (Logistic Regression, KNN, K-Means) really care about feature magnitude. If one column is in the thousands and another is between 0 and 1, the bigger one will dominate the loss function or the distance calculation, even if it isn't the more useful feature. Standardizing fixes that.

The other thing that surprised me was how quickly one-hot encoding can blow up the feature count. In my final project I had a `genre` column with 113 distinct values, and one-hot encoding it pushed the feature count from 14 to 127. That's manageable for tree models but can hurt linear ones if you don't regularize.

## A small thing that tripped me up

I scaled the full dataset *before* doing the train/test split the first time around, which is a leak — the scaler "sees" the test set's statistics. The right pattern is to fit the scaler on the training set only and then apply it to the test set. Looking dumb on this once was probably the best way to remember it.
