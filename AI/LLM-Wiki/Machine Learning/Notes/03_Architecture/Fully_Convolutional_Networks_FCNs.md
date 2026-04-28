---
id: 03-fcns-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Fully Convolutional Networks FCNs

> [!ABSTRACT]
> Fully Convolutional Networks (FCNs) are architectures composed entirely of convolutional and pooling layers, without any dense (fully connected) layers at the top. This allows them to process images of any size and output a spatial map of predictions (e.g., a grid of bounding boxes or a pixel-wise classification map) in a single efficient pass.

## 🧠 Intuition First
- Imagine a standard CNN is like a person who can only recognize a "Dog" if it's perfectly centered in a small polaroid photo. An **FCN** is like a person with a grid of magnifying glasses. They look at a massive landscape once and can tell you exactly which "magnifying glass regions" contain a dog. Instead of moving the polaroid around (sliding window), they see everything at once.

## 🎯 Why This Matters
- Problem it solves: Eliminates the massive redundancy and computational cost of the "sliding window" approach by performing equivalent operations using convolutions on a larger input image.
- Real-world usage: The foundation for real-time object detectors (YOLO) and semantic segmentation models.

## 🧩 Glossary
- [[FCN]] : Fully Convolutional Network.
- [[Sliding Window]] : A technique for processing sub-regions of an image one by one (highly inefficient).
- [[Heatmap]] : A 2D spatial representation of model confidence scores for a particular feature or class.
- [[Valid Padding]] : Using a kernel exactly the size of the input feature map to convert it into a $1 \times 1$ "pixel" with many channels.

## ⚙️ Mechanics (First Principles)
### Converting Dense to Conv:
- Any dense layer can be converted to an equivalent convolutional layer.
- **Rule:** If a dense layer has 200 units and its input is a $7 \times 7 \times 100$ feature map, you replace the dense layer with a Conv2D layer having 200 filters, $7 \times 7$ kernel size, and "valid" padding.
- **Result:** Instead of a flat vector of 200 numbers, the Conv2D layer outputs a $1 \times 1 \times 200$ tensor.

### Processing Larger Images:
- If you feed a $14 \times 14$ image into the same FCN, the converted layer will output an $8 \times 8$ grid of predictions ($14 - 7 + 1 = 8$). Each cell in the grid corresponds to what the original CNN would have seen if it had "slid" over that region.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Converting a model in Keras:
```python
# Assuming original model had Flatten() -> Dense(100)
# New model replaces it with:
# Conv2D(filters=100, kernel_size=final_fmap_size, padding="valid")
```

## 🧪 Experiments
1. **The Efficiency Race:** Compare the time to run a 224x224 CNN on 100 overlapping crops of a 500x500 image vs. running an equivalent FCN once on the full 500x500 image. Observe the orders-of-magnitude speedup.

## ⚠️ Constraints & Pitfalls
- **Spatial Resolution Loss:** Because of pooling and strides, the final output grid is much smaller than the original image (e.g., 32x smaller). This makes precise localization difficult without additional skip connections.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on [[Convolutional_Layers_Mechanics]]
- Used in [[YOLO_Object_Detection]]
- Related to [[Semantic_and_Instance_Segmentation]]
---
(MINIMUM 3 links)
