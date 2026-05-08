# Lab 10 — Unsupervised Learning (K-Means + PCA)

Up to this point everything in the course had been supervised — there were labels and the model learned to predict them. This lab was a switch: no labels, just data, find structure.

## File

- `L10_Trilok_ITAI1371.ipynb`

## What the lab covered

**K-Means clustering** — I used `make_blobs` to generate synthetic data with known clusters, then ran K-Means and checked how well the algorithm recovered the original groups. After that I ran K-Means on the Iris dataset (without using the species labels) and compared the discovered clusters to the actual species.

**PCA** — Principal Component Analysis, which projects high-dimensional data into a lower-dimensional space while keeping as much variance as possible. I used it to take the 4-dimensional Iris features down to 2 dimensions so I could plot them, and the species clusters were still visible in the projection.

## What I took from it

Two big things.

First, K-Means assumes you already know `k`. Picking the right number of clusters is its own problem. The elbow method (plot inertia vs. k and look for the bend) and silhouette score both help, but they don't always agree, and on real messy data the elbow is sometimes more of a slope.

Second, PCA is mostly useful as a *visualization* and *speedup* tool, not as a replacement for the original features. It loses interpretability — your axes are now linear combinations of the original features, which can be hard to explain to anyone.

## Where I used this later

In the final project I ran K-Means on the Spotify audio features to see if songs cluster naturally by sound alone. They sort of do, but the clusters didn't line up cleanly with genre, which was an interesting result on its own.
