---
id: 03-stac-a1b2
tags: [agentic-ai, 03_Architecture, ensemble-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Stacking Ensembles

> [!ABSTRACT]
> Stacking (Stacked Generalization) is an ensemble method where a model (called a blender or meta-learner) is trained to aggregate the predictions of all other predictors. This replaces trivial functions like hard voting with a learned optimization of the individual models' contributions.

## 🧠 Intuition First
- Imagine you have three friends who are good at predicting movie ratings. Friend A likes action, Friend B likes romance, and Friend C likes sci-fi. Instead of just taking the average of their guesses, you track how right each one was on different types of movies. You build a "personal map" (the blender) that says: "When Friend A and C agree, trust them; but if it's a romantic movie, trust Friend B more."

## 🎯 Why This Matters
- Problem it solves: Optimizes the weighting of individual predictors based on their actual performance patterns on a validation set.
- Real-world usage: High-performance predictive systems where multiple distinct algorithms are available.

## 🧩 Glossary
- [[Stacking]] : Stacked Generalization. Using a model to perform the final aggregation.
- [[Blender]] : The final model that takes predictions of other models as input features (also called a **Meta-Learner**).
- [[Out-of-sample Predictions]] : Predictions made by base models on data they did not see during training (crucial for training the blender).

## ⚙️ Mechanics (First Principles)
### The Training Workflow:
1. **Split Data:** Divide the training set into two subsets (or use cross-validation).
2. **Train Base Models:** Train the initial ensemble on Subset 1.
3. **Generate Features:** Use the trained models to make predictions on Subset 2. These predictions become the *new input features* for the blender.
4. **Train Blender:** Train the blender on the new features using the original targets from Subset 2.
5. **Retrain:** Retrain the base models on the full original training set.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.ensemble import StackingClassifier

stacking_clf = StackingClassifier(
    estimators=[('lr', log_reg), ('rf', rnd_clf), ('svc', svm_clf)],
    final_estimator=RandomForestClassifier(),
    cv=5 # Use cross-validation to get out-of-sample predictions
)
stacking_clf.fit(X_train, y_train)
```

## 🧪 Experiments
1. **Blender Impact:** Compare a Voting Classifier with `voting='soft'` against a Stacking Classifier using the same base models. Observe if the blender can find better weights for each model's predictions.

## ⚠️ Constraints & Pitfalls
- **Complexity:** Stacking adds significant overhead to training time and system maintenance.
- **Risk of Overfitting:** The blender itself can overfit the validation predictions if Subset 2 is too small or the blender is too complex.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Voting_Classifiers]]
- Used in → [[ML_Success_Metrics]]
- Related to → [[Boosting_AdaBoost_and_Gradient_Boosting]]
---
(MINIMUM 3 links)
