---
id: 06-enco-a1b2
tags: [agentic-ai, 06_Implementation, data-preparation]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Categorical Encoding

> [!ABSTRACT]
> Machine learning algorithms prefer working with numbers, so categorical (text) attributes must be converted to numerical representations. Common methods include Ordinal Encoding for ordered categories and One-Hot Encoding for unordered ones.

## 🧠 Intuition First
- Imagine a shelf of fruits: apples, oranges, and bananas. 
- **Ordinal Encoding:** You label them 1, 2, and 3. This is like a teacher saying "1 is bad, 2 is okay, 3 is good." The numbers represent an order of quality or rank.
- **One-Hot Encoding:** You create three empty boxes: one labeled "apple," one "orange," and one "banana." If you have an apple, you put a "1" in the apple box and a "0" in the others. There is no rank, just identity.

## 🎯 Why This Matters
- Problem it solves: Converts qualitative information into a format suitable for quantitative analysis.
- Real-world usage: Categorizing country codes, product types, or sentiment (positive/negative).

## 🧩 Glossary
- [[Ordinal Encoding]] : Assigning an integer to each category based on an inherent order.
- [[One-Hot Encoding]] : Creating a binary attribute for each category (only one is "1" or "hot" at a time).
- [[Sparse Matrix]] : A matrix containing mostly zeros, represented efficiently in memory by storing only the locations of nonzero values.
- [[Dummy Attributes]] : The binary features created during one-hot encoding.

## ⚙️ Mechanics (First Principles)
### The Encoding Choice:
1. **Ordinal Encoding:** Best for categories with a natural order (e.g., bad, average, good).
    - *Pitfall:* ML algorithms will assume that "bad" (0) and "average" (1) are more similar than "bad" (0) and "good" (2).
2. **One-Hot Encoding:** Best for categories with no order (e.g., California, Texas, New York).
    - *Mechanics:* Each category gets its own column. Only one column is "1" per row.
    - *Constraint:* Avoid when there are hundreds of categories (causes a "sparse matrix" that might slow down training).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn's `OneHotEncoder`:
```python
from sklearn.preprocessing import OneHotEncoder
cat_encoder = OneHotEncoder()
# Fit and transform training data
housing_cat_1hot = cat_encoder.fit_transform(housing_cat)
# Handle unknown categories in production
cat_encoder.handle_unknown = "ignore"
```

## 🧪 Experiments
1. **The "Similarity" Test:** Train a Linear Regression model on Ordinal Encoded data for unordered categories and observe if the model makes nonsensical predictions for intermediate values.

## ⚠️ Constraints & Pitfalls
- **Accidental Order:** Never use Ordinal Encoding for unordered categories (like city names), as the model will misinterpret the numbers as having a quantitative relationship.
- **Dimensionality:** One-hot encoding on a feature with 1,000 categories will add 1,000 new features to your dataset, potentially leading to the "curse of dimensionality."

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> **Scikit-Learn vs. Pandas:** Pandas `get_dummies()` is convenient but should NOT be used for production pipelines because it doesn't "remember" which categories it was trained on. Use `OneHotEncoder` instead.

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[End_to_End_Project_Checklist]]
- Related to → [[Scikit_Learn_API_Design]]
---
(MINIMUM 3 links)
