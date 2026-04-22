---
id: 04-leak-g7h8
tags: [agentic-ai, 04_Training, data-leakage]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# Data Leakage

> [!ABSTRACT]
> Data leakage occurs when a machine learning model inadvertently has access to information during training that it would not realistically possess during production inference. This leads to an artificially inflated view of the model's performance on validation and test sets, ultimately resulting in severe failures when deployed in the real world.

## 🧠 Intuition First
- Imagine taking a final exam where one of the questions accidentally includes the answer key printed at the bottom of the page. You will score perfectly on that question, but your score doesn't reflect your actual knowledge. If the teacher uses that test to judge your readiness for the next grade, you will likely fail. Data leakage is giving your model the answer key during practice.

## 🎯 Why This Matters
- Problem it solves: Identifying hidden bugs in the data processing and splitting pipeline that compromise the validity of the entire model.
- Real-world usage: Ensuring a medical diagnosis model doesn't secretly learn from a "patient deceased" timestamp feature, or preventing a stock prediction model from accidentally using tomorrow's closing price.

## 🧩 Glossary
- [[Sample Contamination]] : A form of data leakage where data points belonging to the same entity or logical group are split across both the training and validation sets.
- [[Temporal Leakage]] : A form of data leakage where future events are used to predict past or present events in time-series forecasting.

## ⚙️ Mechanics (First Principles)
- **Identify Target:** Determine exactly what the model is trying to predict and when that prediction needs to be made in the real world.
- **Trace Features:** Trace the origin of every feature used in the training set to ensure its value is strictly determined by information available *before* the time of prediction.
- **Isolate Splits:** Ensure the method used to split training, validation, and test data does not allow information from the validation/test sets to bleed into the training process (e.g., through global normalization scaling).
- **Evaluate Surprises:** Treat any model that achieves near-perfect accuracy on a difficult task with extreme skepticism and thoroughly inspect the most predictive features.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Example of avoiding sample contamination using GroupShuffleSplit in Python:
```python
import pandas as pd
from sklearn.model_selection import GroupShuffleSplit

# Dataset with multiple entries per user (author_id)
data = pd.DataFrame({'author_id': [1, 1, 2, 2, 3], 'text': ['a', 'b', 'c', 'd', 'e']})

# A random split might put author 1 in both train and test!
# GroupShuffleSplit ensures all records from a given author stay in the same split.
splitter = GroupShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
train_idx, test_idx = next(splitter.split(data, groups=data['author_id']))

train_data = data.iloc[train_idx]
test_data = data.iloc[test_idx]
```

## 🧪 Experiments
1. **Feature Importance Audit:** Use a tool like Scikit-Learn's `feature_importances_` to analyze a highly accurate model. If one single feature overwhelmingly dominates the prediction, remove it and see if the accuracy plummets—it may be a leaked feature.
2. **Intentional Contamination:** Purposefully leak the target variable into the training set (e.g., multiply the target by 0.5 and add it as a feature) to observe how it distorts the learning process and validation metrics.

## ⚠️ Constraints & Pitfalls
- **Subtle Forms:** Leakage isn't always obvious; it can happen through data preprocessing steps like normalizing the *entire* dataset before splitting it, meaning the training data was scaled using information from the test data.
- **Database Snapshots:** Pulling historical data from a production database that has been overwritten with future states (e.g., a "user_status" field that updated after the historical event occurred) is a very common trap.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Setting_Up_Data]]
- Used in → [[Model_Evaluation]]
- Related to → [[Overfitting]]
