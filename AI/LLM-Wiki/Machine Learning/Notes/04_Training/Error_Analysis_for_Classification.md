---
id: 04-erra-a1b2
tags: [agentic-ai, 04_Training, error-analysis]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Error Analysis for Classification

> [!ABSTRACT]
> Error analysis is the process of identifying why a classifier is failing and determining how to improve it. This involves visualizing the confusion matrix, normalizing it to spot systematic errors, and analyzing individual misclassified instances.

## 🧠 Intuition First
- Imagine you're teaching a child to recognize animals. If the child keeps calling a tiger a "cat," you don't just say they're wrong. You look at *why* they're confused (both have fur, whiskers, and tails). Then you teach them to look for the tiger's stripes. **Error analysis** is identifying those stripes for your model.

## 🎯 Why This Matters
- Problem it solves: Points directly to where the model needs better features or more representative data.
- Real-world usage: Diagnosing why a handwritten digit recognizer confuses 3s and 5s.

## 🧩 Glossary
- [[Normalized Confusion Matrix]] : A confusion matrix where each value is divided by the total number of images in its actual class (to see percentages).
- [[Data Augmentation]] : Generating new training instances by applying slight transformations (like shifting, rotating, or scaling) to existing ones.
- [[Error Weights]] : Artificially increasing the visual weight of errors in a confusion matrix to make them stand out.

## ⚙️ Mechanics (First Principles)
### The 3 Steps of Error Analysis:
1. **Confusion Matrix Visualization:** Plot the matrix to see where the diagonal (correct predictions) is weak.
2. **Normalization:** Divide by the total instances per class. This prevents classes with more data from dominating the visualization.
3. **Specific Error Extraction:** Filter the dataset for specific confusions (e.g., all actual 5s that were predicted as 8s) and visualize them.

### Common Solutions:
- **Feature Engineering:** Count closed loops (e.g., an 8 has two, a 6 has one).
- **Preprocessing:** Centering and rotating images to make them consistent.
- **Data Augmentation:** Force the model to be tolerant of slight shifts and rotations by training on augmented data.

## 📐 Mathematical Foundations
- **Normalized Cell ($C_{i,j}$):**
  $C_{i,j}' = \frac{C_{i,j}}{\sum_{k=1}^{n} C_{i,k}}$

## 💻 Implementation
- Plotting normalized error matrix in Scikit-Learn:
```python
from sklearn.metrics import ConfusionMatrixDisplay

# Show percentages and normalize by row (actual class)
ConfusionMatrixDisplay.from_predictions(y_true, y_pred, 
                                        normalize="true", values_format=".0%")
```

## 🧪 Experiments
1. **The Weight Test:** Plot a confusion matrix where correct predictions are set to zero. Observe how this "brightens" the errors and makes the model's systematic failures obvious.

## ⚠️ Constraints & Pitfalls
- **Symmetry Illusion:** Confusion matrices are NOT symmetrical. For example, a model might misclassify many 5s as 8s, but correctly classify almost all 8s.
- **Over-preprocessing:** Preprocessing can sometimes remove useful signals (e.g., the specific way a person tilts their handwriting).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Metrics]]
- Used in → [[Multiclass_Classification_Strategies]]
- Related to → [[Data_Augmentation]]
---
(MINIMUM 3 links)
