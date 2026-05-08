# Lab 03 — ML Workflow and Types of Learning

This was the first real ML lab of the semester. The goal was to walk through the full machine learning workflow end to end — load data, do a quick EDA, train a model, evaluate it — and to understand the difference between supervised, unsupervised, and reinforcement learning.

## Files

- `L03_Trilok_ITAI1371.pdf` — the lab worksheet I worked through
- `L03Journal_Trilok_ITAI1371.pdf` — my reflective journal for this module

## What the lab covered

The dataset was the classic Wine dataset from sklearn (178 samples, 13 chemical features, 3 wine classes). I built a Logistic Regression and a Decision Tree classifier on it after a train/test split, then compared accuracy.

Key things from the workflow:
- `train_test_split` to separate training and test data
- `StandardScaler` for feature scaling
- `accuracy_score`, `classification_report`, `confusion_matrix` for evaluating the model

## What I actually learned

Honestly, the train/test split is the part that finally clicked for me. I knew you were *supposed* to do it but I couldn't really explain why until I saw training accuracy and test accuracy side by side. A model can memorize the training set and look perfect, and that tells you basically nothing about how it'll do on new data. The test set is the only honest measure.

The other thing that stuck with me was the fraud-detection case study in the reading. I had always pictured fraud detection as a rule-based system, but it makes way more sense as a supervised learning problem — you have labeled past transactions and the model finds the patterns. The catch is that accuracy is a terrible metric there. If 0.1% of transactions are fraud, a model that always says "not fraud" is 99.9% accurate and completely useless. That's what got me curious about precision and recall, which we ended up covering in Lab 07.

## What I want to dig into more

- Cross-validation (a single split still feels arbitrary depending on which samples land where)
- Class imbalance handling — what to actually do when one class is way smaller than the other
- Random Forests — how a bunch of decision trees together end up more reliable than one tree alone
