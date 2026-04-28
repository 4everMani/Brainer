---
id: 04-clea-a1b2
tags: [agentic-ai, 04_Training, data-preparation]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Data Cleaning Strategies

> [!ABSTRACT]
> Data cleaning is the process of handling missing values and outliers in a dataset. Common strategies for missing data include dropping rows/columns or replacing missing values with a statistic (mean, median) or a predicted value (imputation).

## 🧠 Intuition First
- Imagine you're doing a puzzle and some pieces are missing. 
- **Dropping:** You just throw away the whole puzzle because it's incomplete. 
- **Simple Imputation:** You take a piece from a similar puzzle and paint it to look like what you think the missing piece should be (e.g., if you're in the middle of a forest, you paint it green). 
- **Iterative Imputation:** You look at all the surrounding pieces to guess the color and pattern of the missing piece as accurately as possible.

## 🎯 Why This Matters
- Problem it solves: Prevents machine learning models from crashing when they encounter missing data and ensures the model is trained on a representative dataset.
- Real-world usage: Handling sensor failures in IoT data or incomplete customer profiles.

## 🧩 Glossary
- [[Imputation]] : The process of replacing missing data with substituted values.
- [[SimpleImputer]] : A transformer that replaces missing values with a basic statistic (mean, median, most frequent) or a constant value.
- [[KNNImputer]] : Replaces missing values based on the mean of the k-nearest neighbors' values.
- [[IterativeImputer]] : Trains a regression model per feature to predict missing values based on all other available features.

## ⚙️ Mechanics (First Principles)
### Options for Handling Missing Values:
1. **Drop the Rows:** Only if the number of missing rows is very small.
2. **Drop the Column:** Only if the feature is not important for the prediction.
3. **Simple Imputation:** Use the median of the training data (not the test set) to fill the gaps.
    - *Constraint:* Only for numerical attributes.
4. **Advanced Imputation:** Use a model (KNN or Regression) to predict what the missing value should be.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn's `SimpleImputer`:
```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy="median")
# Fit to training data only!
imputer.fit(housing_num)
# Transform both training and test data
X = imputer.transform(housing_num)
```

## 🧪 Experiments
1. **Imputation Comparison:** Intentionally remove 5% of data from a complete dataset. Compare the RMSE of a model trained after simple imputation vs. KNN imputation.

## ⚠️ Constraints & Pitfalls
- **Fit on Train Only:** One of the most common errors is to fit an imputer on the *entire* dataset (leaking test data into the training process). Always fit only on the training set.
- **Categorical Handling:** Simple mean/median imputation doesn't work for categorical data; use "most frequent" or a constant instead.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Main_Challenges_of_Machine_Learning]]
- Used in → [[End_to_End_Project_Checklist]]
- Related to → [[Scikit_Learn_API_Design]]
---
(MINIMUM 3 links)
