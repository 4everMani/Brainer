---
id: 06-pipe-a1b2
tags: [agentic-ai, 06_Implementation, data-preparation]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Column Transformer and Pipelines

> [!ABSTRACT]
> Scikit-Learn's `Pipeline` and `ColumnTransformer` classes allow for the automation and modularization of complex data preparation workflows, ensuring that numerical and categorical attributes are handled correctly and in the right sequence.

## 🧠 Intuition First
- Imagine a factory assembly line. 
- **Pipeline:** This is the sequence of machines. Machine A cleans the parts, Machine B paints them, and Machine C assembles them. The parts move from one to the next automatically.
- **ColumnTransformer:** This is a specialized sorter at the start of the line. It sends all the "metal parts" to the metal-cleaning machine and all the "plastic parts" to the plastic-cleaning machine, then brings them back together for the next step.

## 🎯 Why This Matters
- Problem it solves: Prevents manual, error-prone data preparation steps and ensures that the exact same transformations are applied to both training and test data (or live production data).
- Real-world usage: Handling a dataset with mixed types (e.g., age, income, city, gender) in a single, automated step.

## 🧩 Glossary
- [[Pipeline]] : A sequence of estimators where all but the last must be transformers. It exposes the methods of the final estimator.
- [[ColumnTransformer]] : A transformer that allows different transformers to be applied to different subsets of columns.
- [[make_pipeline]] : A shorthand function to create a pipeline without naming the steps.
- [[make_column_transformer]] : A shorthand function to create a ColumnTransformer without naming the steps.

## ⚙️ Mechanics (First Principles)
### The Full Preprocessing Workflow:
1. **Numerical Pipeline:** Impute missing values -> Scale features (StandardScaler).
2. **Categorical Pipeline:** Impute missing values (Most Frequent) -> One-Hot Encode.
3. **Column Transformer:** Apply the numerical pipeline to numeric columns and the categorical pipeline to text columns.
4. **Final Pipeline:** Combine the Column Transformer with a learning model (e.g., Random Forest).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Full preprocessing pipeline:
```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder

num_pipeline = Pipeline([
    ("impute", SimpleImputer(strategy="median")),
    ("scale", StandardScaler())
])

cat_pipeline = Pipeline([
    ("impute", SimpleImputer(strategy="most_frequent")),
    ("encode", OneHotEncoder(handle_unknown="ignore"))
])

preprocessing = ColumnTransformer([
    ("num", num_pipeline, num_attribs),
    ("cat", cat_pipeline, cat_attribs)
])
```

## 🧪 Experiments
1. **Pipeline Visualization:** Use `sklearn.set_config(display="diagram")` in a Jupyter notebook to visualize a complex pipeline and ensure the steps are in the correct order.

## ⚠️ Constraints & Pitfalls
- **Column Names:** Ensure that `num_attribs` and `cat_attribs` match the column names in your DataFrame.
- **Last Estimator:** If the last estimator in a pipeline is a transformer, the pipeline is a transformer. If it's a predictor, the pipeline is a predictor.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Scikit_Learn_API_Design]]
- Used in → [[End_to_End_Project_Checklist]]
- Related to → [[Custom_Transformers]]
---
(MINIMUM 3 links)
