# Trilok Kalani — ITAI 1371 Machine Learning Portfolio

Houston Community College • Spring 2026

This is the place where I'm keeping all the work I did for ITAI 1371 (Applied Machine Learning). Labs, midterm, final project, and the journal entries that came with them.

## A bit about me

I'm a student at HCC working through the AI/ML track. Coming into this course I had some Python experience but not much hands-on ML, so most of this was new. What I like about ML is that it's one of the few CS topics that forces you to think about the data and the math at the same time — you can't just write code that "compiles and works," you have to actually look at what your model is doing and ask if the result makes sense.

Right now I'm most interested in applied ML in industries that aren't usually thought of as tech-first — real estate, music, healthcare. My midterm and final ended up being in those first two areas, which wasn't planned but worked out.

## How this repo is organized

```
Trilok-Kalani-ML-Course/
├── README.md                ← you are here
├── Labs/                    ← weekly hands-on labs (L03 through L12)
├── Assignments/             ← standalone written assignments
└── Projects/
    ├── Midterm_Project_Real_Estate/
    └── Final_Project_Song_Popularity/
```

Each lab folder has the notebook (or PDF, for L03) plus a short README explaining what the lab covered, what I actually did, and what I took away from it. Assignments has the standalone written deliverables. The two project folders have full code, plots, the written report, and a longer README.

## Labs

| Lab | Topic | What I built |
|-----|-------|--------------|
| [Lab 03](Labs/Lab03/) | ML Workflow + Types of Learning | First classification model on the Wine dataset; reflection journal |
| [Lab 04](Labs/Lab04/) | Exploratory Data Analysis | Distributions, correlations, outliers using seaborn / matplotlib |
| [Lab 05](Labs/Lab05/) | Data Preparation | Scaling, encoding, handling missing values |
| [Lab 06](Labs/Lab06/) | Linear & Logistic Regression | First regression and classification models from scratch using sklearn |
| [Lab 07](Labs/Lab07/) | Better Model Evaluation | Confusion matrix, precision/recall, cross-validation |
| [Lab 08](Labs/Lab08/) | Bias-Variance Tradeoff | Polynomial fits showing overfitting and underfitting visually |
| [Lab 10](Labs/Lab10/) | Unsupervised Learning | K-Means clustering and PCA on the Iris dataset |
| [Lab 11](Labs/Lab11/) | Hyperparameter Tuning + AutoML | GridSearchCV, RandomizedSearchCV, AutoGluon |
| [Lab 12](Labs/Lab12/) | Ethics, Fairness, and Bias | Auditing a real-world model for fairness across demographic groups |

(There was no Lab 09 in the course schedule.)

## Assignments

| # | Assignment | What it was |
|---|------------|-------------|
| [1](Assignments/Assignment1_Github_Repository_Link/) | GitHub Repository Link | First assignment of the semester — set up a public GitHub account and submit the repository link in a one-page Word doc |

## Projects

### Midterm — Listing Engagement Predictor for Real Estate
Built a binary classifier that predicts whether a property listing will land in the top 25% of engagement on a real-estate platform. Compared Logistic Regression, Random Forest, and Gradient Boosting on features like price, square footage, photo count, and days on market. Full write-up and plots in [Projects/Midterm_Project_Real_Estate/](Projects/Midterm_Project_Real_Estate/).

### Final — Song Popularity Prediction Using Spotify Audio Features
Used a Kaggle Spotify dataset with about 114K tracks to predict popularity from audio features (danceability, energy, valence, etc.). Did both regression (predict the 0–100 score) and classification (Low/Medium/High tier), then ran K-Means to look for natural clusters. Best regression hit R² = 0.42 with tuned HistGradientBoosting on audio + genre. The interesting takeaway was how much of popularity really *isn't* in the audio. Details in [Projects/Final_Project_Song_Popularity/](Projects/Final_Project_Song_Popularity/).

## Tools I used

Python 3, Jupyter / Colab, scikit-learn, pandas, numpy, matplotlib, seaborn. AutoGluon for the AutoML lab. Git/GitHub for version control.

## Contact

GitHub: [Tikskalani](https://github.com/Tikskalani)
