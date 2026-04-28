---
id: 06-tvis-a1b2
tags: [agentic-ai, 06_Implementation, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Transfer Learning for Computer Vision

> [!ABSTRACT]
> Transfer learning involves taking a model pretrained on a large, generic dataset (e.g., ImageNet) and adapting it to a smaller, more specific task. This is achieved by reusing the lower layers as a feature extractor and training a new output head, often followed by fine-tuning the base model's top layers.

## 🧠 Intuition First
- Imagine you're building a furniture store. Instead of building the whole store from scratch (training from scratch), you rent an existing building that already has walls, electricity, and plumbing (pretrained model). You only need to add your own signage (new output head) and organize the interior (fine-tuning). You save massive amounts of time and money because the foundation is already there.

## 🎯 Why This Matters
- Problem it solves: Enables the creation of high-accuracy models with very small datasets (e.g., hundreds of images) by leveraging patterns already learned from millions of generic images.
- Real-world usage: Identifying specific plant diseases, classifying custom industrial parts, or specialized medical diagnosis.

## 🧩 Glossary
- [[Frozen Layers]] : Pretrained layers whose weights are not updated during the initial phase of training.
- [[Feature Extractor]] : The base model (without the output head) used to convert raw images into high-level features.
- [[Fine-tuning]] : Unfreezing the top layers of a pretrained base model and retraining them with a very low learning rate.
- [[include_top=False]] : A Keras argument used to load a pretrained model without its final global average pooling and dense classification layers.

## ⚙️ Mechanics (First Principles)
### The 2-Phase Workflow:
1. **Phase 1: Feature Extraction**
    - Load a pretrained model (e.g., Xception) with `include_top=False`.
    - Freeze all layers in the base model.
    - Add a new Global Average Pooling layer and a Dense output layer for your specific classes.
    - Train only the new head for a few epochs.
2. **Phase 2: Fine-Tuning**
    - Unfreeze some or all layers in the base model.
    - Recompile the model with a **much lower learning rate** (e.g., 10x smaller).
    - Continue training until convergence.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Keras transfer learning workflow:
```python
# 1. Load and freeze
base_model = tf.keras.applications.Xception(weights="imagenet", include_top=False)
for layer in base_model.layers: layer.trainable = False

# 2. Add custom head
model = tf.keras.Sequential([
    base_model,
    tf.keras.layers.GlobalAveragePooling2D(),
    tf.keras.layers.Dense(n_classes, activation="softmax")
])

# 3. Train head, then fine-tune top layers of base_model
```

## 🧪 Experiments
1. **The Learning Rate Test:** During fine-tuning, use a high learning rate (e.g., 0.1). Observe how the validation accuracy crashes as the precious pretrained weights are "wrecked" by large updates.

## ⚠️ Constraints & Pitfalls
- **Preprocessing Mismatch:** You MUST use the specific `preprocess_input` function associated with the pretrained model.
- [[Include Top Warning]] : If you set `base_model.trainable = False`, you must still recompile the final model for the change to take effect.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Using_Pretrained_CNN_Models]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Self_supervised_Learning]]
---
(MINIMUM 3 links)
