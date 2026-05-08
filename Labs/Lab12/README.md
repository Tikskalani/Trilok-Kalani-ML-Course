# Lab 12 — Ethics, Fairness, and Bias in ML

This was the lab I expected to be theoretical and ended up being the most uncomfortable one of the semester. The exercise: train a model on a real-world dataset, then audit it for fairness across demographic groups.

## File

- `L12_Trilok_ITAI1371.ipynb`

## What the lab covered

I built a Logistic Regression classifier and then sliced its accuracy and error rates by a sensitive attribute (the lab used a demographic feature). Even when overall accuracy looked solid, the model performed noticeably worse on some subgroups. That's the whole point of the lab — overall accuracy can hide really uneven behavior underneath.

Concepts covered:
- **Demographic parity** — does the model predict positives at the same rate across groups?
- **Equalized odds** — are the false positive and false negative rates the same across groups?
- **Disparate impact** — even if the model isn't using a sensitive attribute directly, are the proxies in the data baking in historical bias?

## What I took from it

The version of fairness you optimize for is itself a value judgment. You can't satisfy every fairness definition at the same time — there are mathematical proofs that show some of them are mutually exclusive. So the question isn't "is my model fair," it's "which fairness criterion matches the harm I'm trying to avoid in *this specific application*?"

The other thing that hit was that bias isn't something you add to a model accidentally with bad code. It comes in through the *data* — historical decisions, who got recorded, who didn't, how labels were assigned. A model trained on biased data will reproduce the bias and probably amplify it through confidence on the majority pattern. Fixing it usually requires going back to the data, not tweaking the model.

This is the lab I think about whenever I see a news story about a deployed ML system going wrong.
