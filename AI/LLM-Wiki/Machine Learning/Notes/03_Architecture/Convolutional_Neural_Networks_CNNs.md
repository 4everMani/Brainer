---
id: 03-cnns-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Convolutional Neural Networks CNNs

> [!ABSTRACT]
> Convolutional Neural Networks (CNNs) are specialized neural networks inspired by the structure of the biological visual cortex. They excel at processing data with a grid-like topology, such as images, by using local receptive fields and weight sharing to detect hierarchical patterns while significantly reducing the number of model parameters.

## 🧠 Intuition First
- Imagine you're trying to identify a puzzle by looking through a small magnifying glass that only shows one square inch at a time. You slide the glass across the whole puzzle (convolution). First, you only see tiny edges. Then, you combine those edges into shapes, and finally, those shapes into the full picture. Because you use the *same* magnifying glass everywhere, you only need to learn what an "edge" looks like once, rather than learning it for every single spot on the table.

## 🎯 Why This Matters
- Problem it solves: Overcomes the "Parameter Explosion" of fully connected networks on large images and provides **Translation Invariance** (recognizing an object regardless of its position in the frame).
- Real-world usage: Face recognition, autonomous driving (detecting pedestrians), and medical imaging.

## 🧩 Glossary
- [[Visual Cortex]] : The part of the brain that processes visual information, organized into layers of neurons responding to local receptive fields.
- [[Receptive Field]] : The small region of the visual field that a single neuron reacts to.
- [[Weight Sharing]] : Using the same set of weights (a filter) for all neurons in a feature map to reduce parameters.
- [[LeNet-5]] : The 1998 pioneering CNN architecture by Yann LeCun for handwritten digit recognition.

## ⚙️ Mechanics (First Principles)
### Why CNNs beat MLPs for images:
- **MLP Limitation:** A $100 \times 100$ RGB image has 30,000 inputs. A hidden layer with 1,000 neurons would have 30 million connections. This doesn't scale to high-res photos.
- **CNN Solution:**
    1. **Locally Connected Layers:** Neurons only look at a small neighborhood of pixels.
    2. **Hierarchical Learning:** Lower layers detect edges; higher layers detect eyes, ears, or wheels.
    3. **Weight Sharing:** If a filter can detect a vertical line in the top-left corner, it can also detect one in the bottom-right.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- High-level architecture summary:
```python
# Input -> [Conv + ReLU -> Pooling] * N -> Flatten -> Dense -> Output
```

## 🧪 Experiments
1. **The Parameter Count:** Compare the number of trainable weights in a Conv2D layer with 32 filters of size $3 \times 3$ vs. a Dense layer with 32 neurons, both processing a $28 \times 28$ image. Observe how much smaller the CNN layer is.

## ⚠️ Constraints & Pitfalls
- **High RAM Usage:** While parameter count is low, the memory needed to store intermediate feature maps during training is very high.
- **Axis Sensitivity:** Basic CNNs are sensitive to rotation and scaling (though pooling helps with small shifts).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Multilayer_Perceptrons_and_DNNs]]
- Used in → [[Convolutional_Layers_Mechanics]]
- Related to → [[Pooling_Layers_Mechanics]]
---
(MINIMUM 3 links)
