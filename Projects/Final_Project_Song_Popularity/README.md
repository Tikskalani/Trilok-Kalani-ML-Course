# Final Project — Predicting Song Popularity from Spotify Audio Features

Can audio features alone predict how popular a song will be on Spotify? Or is most of popularity driven by things outside the audio — artist reputation, marketing, playlist placement, virality?

That's the question I tried to answer.

## Why this topic

I listen to a lot of music, and I'd been curious for a while whether the actual sound of a song carries a measurable signal for popularity, or whether it's mostly drowned out by everything else. Spotify, Apple Music, and TikTok all rely on audio-feature models for parts of their recommendation pipeline, so this is a real industry question and not just a class exercise.

It also lined up well with the course because the dataset gives you both regression and classification angles cleanly, plus a reason to use unsupervised methods (clustering songs by sound).

## Dataset

The `Spotify Tracks Dataset` from Kaggle (maharshipandya). About 114,000 tracks across 125 genres, with the audio features Spotify exposes through their Web API and a popularity score from 0 to 100.

After deduplicating on `track_id` (the same song appears multiple times because of multi-genre listings), I ended up with 89,740 unique tracks across 113 genres.

**Features I used.** danceability, energy, loudness, speechiness, acousticness, instrumentalness, liveness, valence, tempo, duration_ms, key, mode, time_signature, explicit flag, and (for one experiment) one-hot encoded genre.

**Targets.**
- Regression: `popularity` (0–100)
- Classification: `popularity_tier` (Low / Medium / High, made by binning the score)

## What I built

The pitch deck `FinalPresentation_Trilok_ITAI1371.pptx` walks through the full project visually. The topic-selection PDF `Final_Project_Topic_Selection.pdf` has the literature review and project framing.

**Two feature sets** — to actually measure how much genre matters on top of audio:
- Set A: audio only (14 features)
- Set B: audio + one-hot genre (127 features)

**Models.**
- Regression: Linear, Ridge, Random Forest, HistGradientBoosting
- Classification: Logistic, Decision Tree, Random Forest, HistGradientBoosting
- Unsupervised: K-Means with elbow + silhouette score

**Evaluation.** 80/20 split with fixed seed. RMSE / MAE / R² for regression. Accuracy and weighted F1 for classification. Per-genre prediction error as a fairness check.

**Tuning.** GridSearchCV on the best regression model.

## Results

| Model | Features | R² |
|-------|----------|-----|
| Linear Regression | Audio only | 0.03 |
| Random Forest | Audio only | 0.23 |
| Linear Regression | Audio + Genre | 0.32 |
| HistGradientBoosting (tuned) | Audio + Genre | **0.42** |

Best classification model: tuned HistGradientBoosting at 70% accuracy, F1 = 0.70.

## What the numbers actually mean

The interesting story is in the gap between linear-audio (0.03) and Random Forest on the same features (0.23). Same data, but the tree ensemble finds non-linear patterns that linear models can't see. So the audio carries some signal — you just can't get to it with a straight line.

But the single biggest jump in the whole project was *adding genre*. Linear regression goes from 0.03 to 0.32 just from including the one-hot genre column. That's because genre carries the per-genre baseline popularity (some genres just chart higher than others on average), which the audio features alone can't reconstruct.

The tuned HistGradientBoosting on audio + genre reached R² = 0.42 with RMSE around 15.6. So roughly 42% of popularity variance is explainable from this feature set, and **about 58% is coming from things outside the dataset** — marketing, virality, playlist placement, who the artist is, when the song was released, what's trending culturally.

That last finding is honestly more interesting to me than the R² number. It says audio features have a real ceiling on this problem, and the next big jump in performance probably won't come from a fancier model — it'll come from features about the *artist* and the *time* the song was released.

## Challenges

A few real ones I ran into:

1. **First dataset was synthetic.** My first download looked legit but every model was predicting popularity = 50 for every song. When I checked the data, every audio feature had identical mean and std, and every correlation was 0.00. Not real Spotify data. Had to find a different source.
2. **Tree models were slow.** Standard `GradientBoosting` took forever on 89K rows × 127 features. Switched to `HistGradientBoosting`, which uses histogram binning under the hood, and got about a 10x speedup with slightly better accuracy.
3. **Data leakage from duplicates.** Same `track_id` appearing under multiple genres in the raw data meant the same song could end up in both train and test if I wasn't careful. Deduplicating on `track_id` before splitting fixed it.
4. **Heavily skewed target.** About 11% of tracks have popularity = 0 (catalog tracks no one streams). Considered dropping them but kept them in — they're real data and pretending they aren't there would inflate the model's apparent performance.

## What I'd do next

- **Artist features.** Per-artist mean popularity and total track count. Probably the single biggest gain — right now my model has no idea Drake songs do better than mine before either of us has played a note.
- **Temporal features.** Days since release, weekday vs. weekend release, whether the release window overlapped a major holiday or chart cycle.
- **Lyrics-based NLP.** Sentiment, themes, language, repetition patterns. Audio captures *sound* but not *what the song is about*.
- **Temporal holdout split.** Train on pre-2023 songs and test on 2024 songs. The random split I used probably overstates how well the model generalizes to genuinely new releases.

## Files

- `FinalPresentation_Trilok_ITAI1371.pptx` — final pitch presentation (10 slides)
- `Final_Project_Topic_Selection.pdf` — topic selection write-up with the literature review

## Honest disclosure

I used AI tools as a study aid during this project — checking sklearn syntax, debugging plot code, and reviewing my writing for clarity. All modeling decisions, the experimental design (Set A vs. Set B), the deduplication choice, and the interpretation of results are my own.
