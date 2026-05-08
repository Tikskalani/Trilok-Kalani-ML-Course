# Midterm Project — Listing Engagement Predictor for Real Estate

A binary classifier that predicts whether a real-estate property listing will land in the top 25% of user engagement, based on listing features and metadata.

## Why this problem

Real-estate platforms like Zillow, Redfin, and Realtor.com all use ML behind the scenes to rank listings, surface "hot homes," and give sellers feedback on listing quality. The same listing can do well or poorly depending on a long list of factors that aren't always obvious — price relative to the neighborhood, photo count, description length, days on market. I wanted to see how much of the engagement story is really in the listing data itself versus everything happening outside of it (marketing, agent reach, market timing).

This was also a good fit for the course because the public Kaggle real-estate datasets give you a clean classification setup once you binarize the engagement metric.

## The setup

**Target.** Binary label — `1` if the listing is in the top 25% of engagement (views / saves / inquiries), else `0`.

**Features.**
- Numeric: price, square footage, bedrooms, bathrooms, days on market, photo count, description length
- Categorical: property type, state / region, listing status

**Split.** 80/20 train/test with a fixed random seed for reproducibility. Class imbalance was 75/25, so I tracked F1 and ROC-AUC alongside accuracy.

## Approach

The notebook (`Listing_Engagement_Predictor.ipynb`) walks through everything in order, with plots saved as `plot_01_*.png` through `plot_09_*.png`.

1. **EDA.** Class distribution, feature distributions, state-level analysis, correlation heatmap.
2. **Data cleaning.** Dropped or imputed missing values, removed obvious outliers in price, log-transformed the heavily skewed columns.
3. **Encoding + scaling.** One-hot encoding on categoricals, `StandardScaler` on numerics for the linear model.
4. **Models compared.**
   - Logistic Regression (baseline)
   - Decision Tree
   - Random Forest
   - Gradient Boosting
5. **Evaluation.** Accuracy, precision, recall, F1, ROC-AUC, confusion matrix per model.
6. **Tuning.** GridSearchCV on the best base model.

## Results

Random Forest and Gradient Boosting both clearly beat the linear baseline. The full model-comparison plot is in `plot_05_model_comparison.png`. ROC curves for each model are in `plot_07_roc_curves.png`.

Top features (from the tuned tree-based model, see `plot_08_feature_importance.png`):
- Photo count
- Days on market
- Price per square foot
- Description length

The "photo count matters a lot" finding lines up with what Zillow has published about listing quality — listings with more (and better) photos consistently get more engagement. Days on market is a bit of a chicken-and-egg signal: low DOM tends to mean a hot listing, but it's also being directly observed.

## What I learned

- **The metric you optimize for matters more than the model you pick.** Once I switched from optimizing accuracy to optimizing F1, the ranking of my models actually changed.
- **Feature engineering > model swapping.** Going from price + square footage to "price per square foot" gave a bigger jump than swapping any model for the next-fancier one.
- **Tuning gives you the last few points.** GridSearchCV on Random Forest moved F1 by about 0.02 — real but small. Most of the win came from data work.

## Files

- `Listing_Engagement_Predictor.ipynb` — the full notebook
- `Project_Report.docx` — the written report
- `cleaned_df.csv` — cleaned dataset used by the notebook
- `plot_01_*` through `plot_09_*` — saved figures referenced by the report
- `Supplementary_AI_and_Diagram.pdf` — supplementary diagrams
- `AI_Tools_Disclosure.docx` — required disclosure of AI tool use during the project

## Honest disclosure

I used AI tools as a study and code-review aid during this project (formatting plots, checking sklearn syntax, drafting the writeup). All modeling decisions, feature choices, and result interpretation are my own. Details are in `AI_Tools_Disclosure.docx`.
