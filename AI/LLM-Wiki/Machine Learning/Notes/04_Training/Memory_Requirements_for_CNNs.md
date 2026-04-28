---
id: 04-ramc-a1b2
tags: [agentic-ai, 04_Training, neural-networks]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Memory Requirements for CNNs

> [!ABSTRACT]
> training CNNs requires a significant amount of RAM, primarily due to the need to store all intermediate feature maps during the forward pass for use in the reverse pass of backpropagation. While CNNs have fewer parameters than fully connected layers, their memory footprint during training is often several orders of magnitude larger.

## 🧠 Intuition First
- Imagine you're building a tower of blocks. 
- **Inference (Making a prediction):** You only need to hold the block you just picked up and the top of the tower. Once a floor is built, you can forget the individual blocks.
- **Training (Learning):** You need to remember the *exact* position and color of every single block in the entire tower so you can calculate how to adjust them if the tower starts leaning. You can't let go of any information until the very last block is placed and the error is calculated. This "holding on to everything" is what consumes all the memory.

## 🎯 Why This Matters
- Problem it solves: Explains why large batch sizes or high-resolution images often cause "Out of Memory" (OOM) errors even on powerful GPUs.
- Real-world usage: Essential for sizing hardware for deep learning projects and choosing optimal batch sizes.

## 🧩 Glossary
- [[Feature Map Footprint]] : The total memory occupied by the output of a convolutional or pooling layer (Height $\times$ Width $\times$ Channels $\times$ bits_per_float).
- [[OOM]] : Out of Memory error. A common crash when training large models on GPUs.
- [[Float Precision]] : The number of bits used to represent a number (e.g., 32-bit vs. 16-bit floats).
- [[Batch Dimension]] : The multiplier for memory usage; training with batch size 100 uses 100x more memory for feature maps than batch size 1.

## ⚙️ Mechanics (First Principles)
### Memory Calculation Example:
- **Layer:** 200 filters, $5 \times 5$ kernel, "same" padding, stride 1.
- **Input:** $150 \times 100$ RGB image.
- **Output Tensor:** $150 \times 100 \times 200$.
- **Per Instance Memory:** $150 \times 100 \times 200 \times 32 \text{ bits} = 9.6 \text{ million bits} \approx 1.2 \text{ MB}$.
- **Batch of 100 Memory:** $120 \text{ MB}$ just for this single layer's activations.
- **Total:** A deep network with 10 such layers would require $> 1.2 \text{ GB}$ of RAM during training.

## 📐 Mathematical Foundations
- **Total Training Memory:** 
  $M_{total} \approx \sum_{layers} (M_{parameters} + M_{gradients} + \text{batch\_size} \cdot M_{activations})$

## 💻 Implementation
- Strategies to reduce memory usage:
1. **Reduce Batch Size:** The simplest way to fit a model into RAM.
2. **Increase Stride:** Reduces the spatial resolution (H x W) of feature maps early.
3. **Mixed Precision:** Use 16-bit floats (`float16`) instead of 32-bit.
4. **Remove Layers:** Simplify the architecture.

## 🧪 Experiments
1. **The OOM Threshold:** On a GPU with 8GB RAM, try training a ResNet-50 with batch size 8, 16, 32, 64, and 128. Record the point where the system crashes with an OOM error.

## ⚠️ Constraints & Pitfalls
- **Inference vs Training:** Inference uses much less memory because it can discard feature maps as soon as the next layer is computed. Never size your training hardware based on inference benchmarks.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Convolutional_Layers_Mechanics]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Pooling_Layers_Mechanics]]
---
(MINIMUM 3 links)
