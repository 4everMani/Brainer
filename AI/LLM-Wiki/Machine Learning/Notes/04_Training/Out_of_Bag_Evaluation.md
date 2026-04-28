---
id: 04-oobv-a1b2
tags: [agentic-ai, 04_Training, ensemble-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Out of Bag Evaluation

> [!ABSTRACT]
> In Bagging, for any given predictor, some training instances are used many times, while others are not used at all. On average, only 63% of instances are sampled for each predictor. The remaining 37% are called "Out-of-Bag" (OOB) instances and can be used to evaluate the ensemble without the need for a separate validation set.

## 🧠 Intuition First
- Imagine you're holding 1,000 independent mock exams for a group of students. For each exam, you pick 100 questions from a master list with replacement. For any single exam, some questions from the master list were never picked. You can use those "unseen" questions to test how well that specific exam prepared the student, without needing to go find a whole new set of questions.

## 🎯 Why This Matters
- Problem it solves: Allows for a reliable evaluation of model performance while using the entire training set for training, which is particularly useful when data is scarce.
- Real-world usage: Automatic performance estimation in Random Forests.

## 🧩 Glossary
- [[OOB Instances]] : The training instances that were not sampled during the creation of a particular predictor in a bagging ensemble.
- [[OOB Score]] : The evaluation metric (e.g., accuracy) calculated by testing each instance on the predictors that did not see it during training.
- [[OOB Decision Function]] : The class probabilities for each training instance as estimated by the predictors that did not see it.

## ⚙️ Mechanics (First Principles)
### The 63% Rule:
- As the number of training instances $m$ grows, the probability of an instance *not* being picked in a bootstrap sample of size $m$ converges to $1/e \approx 37\%$.
- Thus, for each predictor, about 37% of the training instances are "Out-of-Bag."

### The Evaluation Process:
1. For each instance in the training set, identify the subset of predictors that did **not** use it during training.
2. Get the ensemble prediction for that instance using only those predictors.
3. Compare the ensemble predictions to the actual targets to calculate the OOB Score.

## 📐 Mathematical Foundations
- **Probability of not being sampled:**
  $P(\text{not sampled}) = (1 - 1/m)^m \approx e^{-1} \approx 0.368$ (for large $m$).

## 💻 Implementation
- Enabling OOB evaluation in Scikit-Learn:
```python
from sklearn.ensemble import BaggingClassifier

bag_clf = BaggingClassifier(
    DecisionTreeClassifier(), n_estimators=500,
    bootstrap=True, n_jobs=-1, oob_score=True
)
bag_clf.fit(X_train, y_train)

# The evaluation score is stored here
print(bag_clf.oob_score_)
```

## 🧪 Experiments
1. **OOB vs Test Accuracy:** Compare the `oob_score_` of a Bagging Classifier with its final accuracy on a held-out test set. They should be very close.

## ⚠️ Constraints & Pitfalls
- **Bootstrap Only:** OOB evaluation only works when `bootstrap=True` (Bagging). It is not possible with Pasting.
- **Small Ensembles:** If you only have a few predictors, some instances might not be OOB for *any* of them, making the evaluation less stable.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Bagging_and_Pasting]]
- Used in → [[Ensemble_Modeling]]
- Related to → [[Testing_and_Validating_Models]]
---
(MINIMUM 3 links)
