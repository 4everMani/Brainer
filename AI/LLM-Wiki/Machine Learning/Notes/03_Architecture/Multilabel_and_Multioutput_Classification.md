---
id: 03-mlla-a1b2
tags: [agentic-ai, 03_Architecture, classification]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Multilabel and Multioutput Classification

> [!ABSTRACT]
> Multilabel classification assigns multiple binary tags to each instance (e.g., recognizing several faces in a single photo). Multioutput classification is a generalization where each label can be multiclass, often used for tasks like image denoising.

## 🧠 Intuition First
- Imagine a photo-tagging system. 
- **Multilabel:** You look at a picture and say "It's a cat" AND "It's outdoors." It's not one or the other—it's both. You output [Cat: True, Outdoors: True, Dog: False].
- **Multioutput:** You look at a noisy picture and, for every single pixel, you predict its correct color (0-255). It's many "labels" (pixels), and each label has many "choices" (colors).

## 🎯 Why This Matters
- Problem it solves: Handles complex data that belongs to more than one category or where the output is a high-dimensional vector.
- Real-world usage: Face tagging in photos, keyword tagging for articles, image restoration.

## 🧩 Glossary
- [[Multilabel Classification]] : A system that outputs a vector of binary tags for each instance.
- [[Multioutput Classification]] : A system where each of multiple labels can be multiclass.
- [[ClassifierChain]] : A strategy for multilabel classification where each model uses the predictions of previous models as additional features.
- [[Hamming Loss]] : A common metric for multilabel classification, measuring the fraction of wrong labels.

## ⚙️ Mechanics (First Principles)
### The Hybrid Approach:
1. **Multilabel:** You can train one model per label independently.
    - *Problem:* This doesn't capture dependencies (e.g., if "Outdoors" is true, it's more likely "Cat" is also true).
2. **ClassifierChain:** Models are organized in a chain. The 1st model predicts Label 1. The 2nd model predicts Label 2 using input features + the 1st model's prediction. This captures dependencies between labels.

### Multioutput Example:
- **Image Denoising:** Input is a noisy image (e.g., $28 \times 28$ pixels). Output is $784$ labels, each with $256$ possible values ($0-255$).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn's `KNeighborsClassifier` for multilabel:
```python
from sklearn.neighbors import KNeighborsClassifier

# Two binary labels for MNIST: Is digit large (7,8,9)? Is digit odd?
y_multilabel = np.c_[y_train_large, y_train_odd]

knn_clf = KNeighborsClassifier()
knn_clf.fit(X_train, y_multilabel)
# Predicts [False, True] for digit 5
```

## 🧪 Experiments
1. **The Chain Advantage:** Compare a multilabel classifier that predicts each label independently versus a `ClassifierChain`. Evaluate their overall F1 score on a dataset with correlated labels.

## ⚠️ Constraints & Pitfalls
- **Model Support:** Not all Scikit-Learn classifiers support multilabel classification natively (e.g., SVC and LogisticRegression do not). Use `ClassifierChain` or `OneVsRestClassifier` to adapt them.
- **Evaluation Difficulty:** Averaging scores across labels is complex. You can use `macro` (average F1) or `weighted` (based on label support).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Basics]]
- Used in → [[Error_Analysis_for_Classification]]
- Related to → [[Multiclass_Classification_Strategies]]
---
(MINIMUM 3 links)
