# Lab 07 — Better Model Evaluation

Accuracy alone is a misleading metric, especially when classes are imbalanced. This lab was about moving past it and using evaluation tools that actually tell you something useful.

## File

- `L07_Trilok_ITAI1371.ipynb`

## What the lab covered

- Confusion matrix — true positives, false positives, true negatives, false negatives
- Precision (of the things the model called positive, how many actually were)
- Recall (of the actual positives, how many did the model catch)
- F1 score as a balance between the two
- Cross-validation using `cross_val_score`

## What I learned

This was the lab where the fraud-detection point from Lab 03 finally made full sense. I built a model and ran it through `cross_val_score` with cv=5, and the variance between the folds was bigger than I expected. That made me trust a single train/test split a lot less than I used to.

Precision and recall are actually two different questions about the same model:
- **Precision** is for when false positives are expensive. (Spam filters: don't flag real emails.)
- **Recall** is for when false negatives are expensive. (Cancer screening: don't miss sick patients.)

You almost never get to maximize both. The F1 score is fine as a default, but in real use cases you usually want to pick the one that matches the cost of the mistake.

## Where I used this later

The midterm project leaned on this hard. The engagement classes were imbalanced (top 25% vs. bottom 75%), so I tracked precision, recall, and F1 instead of just accuracy. The ROC curves in the midterm came from this same headspace.
