---
id: 03-mult-a1b2
tags: [agentic-ai, 03_Architecture, classification]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Multiclass Classification Strategies

> [!ABSTRACT]
> Multiclass (or multinomial) classifiers can distinguish between more than two classes. Binary classifiers can be used for multiclass tasks through strategies like One-versus-the-Rest (OvR) and One-versus-One (OvO).

## 🧠 Intuition First
- Imagine you're at a zoo with 10 different animals. 
- **One-versus-the-Rest (OvR):** You ask 10 questions: "Is it a lion?" "Is it a tiger?" "Is it a zebra?" You pick the animal that gets the most "Yes" votes.
- **One-versus-One (OvO):** You hold 45 duels: "Lion vs. Tiger," "Lion vs. Zebra," "Tiger vs. Zebra," and so on. The animal that wins the most duels is your classification.

## 🎯 Why This Matters
- Problem it solves: Allows binary-only algorithms (like Support Vector Machines) to solve problems with many possible outcomes.
- Real-world usage: Handwritten digit recognition (0-9), face detection (many names).

## 🧩 Glossary
- [[OvR]] : One-versus-the-Rest (also called OvA - One-versus-All). Train N binary classifiers for N classes.
- [[OvO]] : One-versus-One. Train $N \times (N-1) / 2$ binary classifiers for every pair of classes.
- [[Decision Score]] : The value output by each binary classifier used to determine the final multiclass winner.

## ⚙️ Mechanics (First Principles)
### The Strategy Choice:
1. **OvR:** Preferred for most algorithms because it requires fewer classifiers (N). 
    - *Mechanics:* Each classifier predicts "Class X" vs. "Not Class X."
2. **OvO:** Preferred for algorithms that scale poorly with the number of instances (like SVM). 
    - *Mechanics:* Each classifier is trained on only a small subset of the training set (the two classes it's comparing).

### Scikit-Learn Automation:
- Scikit-Learn automatically detects when you try to use a binary classifier for a multiclass task and runs OvR or OvO based on the algorithm's characteristics.

## 📐 Mathematical Foundations
- **Number of OvO Classifiers:** $N \times (N - 1) / 2$
- **Total OvR Classifiers:** $N$

## 💻 Implementation
- Using Scikit-Learn to force OvR:
```python
from sklearn.multiclass import OneVsRestClassifier
from sklearn.svm import SVC

# Forces SVM to use OvR instead of its default OvO
ovr_clf = OneVsRestClassifier(SVC())
ovr_clf.fit(X_train, y_train)
```

## 🧪 Experiments
1. **The Duo Duel:** Count how many binary classifiers are trained for a 4-class problem using OvO ($4 \times 3 / 2 = 6$) versus OvR ($4$).

## ⚠️ Constraints & Pitfalls
- **OvO Computational Cost:** For 1,000 classes, OvO requires roughly 500,000 binary classifiers, which can be extremely slow even if each is small.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Basics]]
- Used in → [[Error_Analysis_for_Classification]]
- Related to → [[Multilabel_and_Multioutput_Classification]]
---
(MINIMUM 3 links)
