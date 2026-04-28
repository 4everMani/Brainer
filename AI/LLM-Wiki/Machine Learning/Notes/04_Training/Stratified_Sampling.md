---
id: 04-stra-a1b2
tags: [agentic-ai, 04_Training, sampling]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Stratified Sampling

> [!ABSTRACT]
> Stratified sampling is a method of dividing the population into homogeneous subgroups called strata, and then sampling the correct number of instances from each stratum to ensure the sample is representative of the overall population.

## 🧠 Intuition First
- Imagine you want to poll US voters, who are 51.1% female and 48.9% male. If you pick 1,000 people purely at random, you might end up with a group that is 60% male by chance, which would bias your result. To prevent this, you intentionally select exactly 511 females and 489 males to match the population's true ratio.

## 🎯 Why This Matters
- Problem it solves: Prevents sampling bias, which is especially critical when the dataset is small relative to the number of attributes.
- Real-world usage: Ensuring that a medical study includes a representative mix of ages or that a housing price model correctly represents both low and high-income districts.

## 🧩 Glossary
- [[Strata]] : Homogeneous subgroups within a population (e.g., income categories or gender).
- [[Sampling Bias]] : A flaw in the data collection process that makes a sample unrepresentative.
- [[Purely Random Sampling]] : A method where every instance in the population has an equal chance of being selected.

## ⚙️ Mechanics (First Principles)
- **Identify Important Attribute:** Choose a feature (e.g., median income) that is critical for the prediction.
- **Categorize (if continuous):** If the attribute is continuous, divide it into discrete categories (e.g., using `pd.cut()` to create 5 income categories).
- **Maintain Proportions:** Ensure that each category (stratum) is large enough and has a proportional number of instances in both the training and test sets.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.model_selection import StratifiedShuffleSplit

# Assuming 'income_cat' is already created
split = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
for train_index, test_index in split.split(housing, housing["income_cat"]):
    strat_train_set = housing.loc[train_index]
    strat_test_set = housing.loc[test_index]
```

## 🧪 Experiments
1. **Bias Check:** Generate two test sets: one using purely random sampling and one using stratified sampling. Compare the percentage of each category in the test sets vs. the full dataset.

## ⚠️ Constraints & Pitfalls
- **Over-stratification:** Creating too many strata or having a stratum that is too small can lead to biased estimates.
- **Wrong Choice of Strata:** Stratifying based on an irrelevant attribute will not improve (and might even harm) model generalization.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Testing_and_Validating_Models]]
- Used in → [[Main_Challenges_of_Machine_Learning]]
- Related to → [[Data_Snooping_Bias]]
---
(MINIMUM 3 links)
