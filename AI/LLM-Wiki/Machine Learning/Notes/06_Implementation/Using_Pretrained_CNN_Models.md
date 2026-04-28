---
id: 06-upre-a1b2
tags: [agentic-ai, 06_Implementation, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Using Pretrained CNN Models

> [!ABSTRACT]
> Keras provides access to several state-of-the-art vision models pretrained on the ImageNet dataset via the `tf.keras.applications` package. These models can be used out-of-the-box for high-accuracy image classification or as base models for transfer learning, significantly reducing the data and compute required for new tasks.

## 🧠 Intuition First
- Imagine you need an expert to sort thousands of photos. Instead of hiring someone off the street and training them for years (training from scratch), you hire an experienced photographer (pretrained model). They already know what dogs, cars, and buildings look like. You just need to show them a few examples of your specific task, and they'll adapt their existing knowledge instantly.

## 🎯 Why This Matters
- Problem it solves: Eliminates the need for massive labeled datasets and weeks of GPU time to build effective computer vision models.
- Real-world usage: Building production-ready image classifiers in hours instead of months.

## 🧩 Glossary
- [[tf.keras.applications]] : A Keras package containing pretrained architectures and weights.
- [[preprocess_input]] : A model-specific function that scales and formats raw images to match the model's training expectations.
- [[decode_predictions]] : A utility that converts the raw probability output of an ImageNet model into human-readable class names.
- [[Top-1 Accuracy]] : The accuracy of the model's most confident prediction.

## ⚙️ Mechanics (First Principles)
### The 3-Step Process:
1. **Load Model:** Instantiate a class from `tf.keras.applications` with `weights="imagenet"`.
2. **Preprocess:** 
    - Resize images to the model's target size (e.g., $224 \times 224$ for ResNet).
    - Use the model's `preprocess_input()` function.
3. **Predict:** Call `model.predict()` and use `decode_predictions()` to get the class labels.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Classifying images with ResNet-50:
```python
import tensorflow as tf

# 1. Load model
model = tf.keras.applications.ResNet50(weights="imagenet")

# 2. Preprocess (X is a batch of raw RGB images)
X_resized = tf.image.resize(X, [224, 224])
X_final = tf.keras.applications.resnet50.preprocess_input(X_resized)

# 3. Predict
Y_proba = model.predict(X_final)
top_3 = tf.keras.applications.resnet50.decode_predictions(Y_proba, top=3)
```

## 🧪 Experiments
1. **The Model Zoo Test:** Compare the predictions of `MobileNetV2` (very small) and `EfficientNetB7` (very large) on the same ambiguous image. Observe the confidence scores and the time taken for inference.

## ⚠️ Constraints & Pitfalls
- [[Preprocessing Mismatch]] : Using the wrong `preprocess_input` function (e.g., using ResNet preprocessing for an Inception model) will result in garbage predictions.
- **Fixed Vocabulary:** These models only recognize the 1,000 ImageNet classes by default. If your object isn't on that list, the model will pick the "closest" looking class.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[EfficientNet_and_Compound_Scaling]]
- Used in → [[ML_Success_Metrics]]
- Related to → [[Transfer_Learning_for_Computer_Vision]]
---
(MINIMUM 3 links)
