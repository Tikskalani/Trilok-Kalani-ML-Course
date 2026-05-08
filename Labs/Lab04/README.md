# Lab 04 — Exploratory Data Analysis (EDA)

This lab was about looking at a dataset *before* trying to model anything. The metaphor in the lab was being a detective — you go in looking for clues that will help you build a better model later.

## File

- `L04_Trilok_ITAI1371.ipynb`

## What I did

The lab was mostly pre-coded so I could focus on reading the visualizations and understanding what to look for. I worked through:

- Summary statistics (`.describe()`, `.info()`) to get a feel for ranges and missing values
- Distribution plots (histograms, boxplots) for individual numeric features
- A correlation heatmap to spot which features move together
- Categorical breakdowns using seaborn (countplot, barplot)

## What I took away

Two things stood out.

First, EDA is where you catch the issues that will wreck your model later — outliers, weird distributions, columns that turn out to be ID fields, classes that are way more imbalanced than you assumed. A lot of "model not working" problems are actually data problems you didn't notice up front.

Second, correlation is helpful but it's not the same as importance. Two features can both be correlated with the target but be redundant with each other. The heatmap showed me which pairs were almost the same column with a different name, which matters when you start picking features for a model.

I came back to this stuff a lot during the midterm and final, where the EDA step ended up being maybe a third of the total work.

## Tools used

`pandas`, `seaborn`, `matplotlib`
