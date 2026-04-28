---
id: 03-vitx-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Vision Transformers ViT

> [!ABSTRACT]
> Vision Transformers (ViT) adapt the transformer architecture for image processing by treating an image as a sequence of small, fixed-size patches. Each patch is flattened and projected into a linear embedding space, mimicking the word embeddings used in NLP. While they lack the strong spatial inductive biases of CNNs, ViTs can outperform them when trained on massive amounts of data.

## 🧠 Intuition First
- Imagine you're identifying a photo of a dog. 
- **CNN:** You use a magnifying glass to scan every inch for edges and textures, slowly building up to the whole dog.
- **ViT:** You cut the photo into 100 small squares (patches) and throw them into a pile. You then look at all the squares at once and use a set of "magic wires" (self-attention) to find how each square relates to every other square. By seeing all the pieces simultaneously, you can understand the "big picture" of the dog instantly, without having to scan linearly.

## 🎯 Why This Matters
- Problem it solves: Provides a unified architecture for both NLP and computer vision, and achieves higher state-of-the-art accuracy on large datasets compared to traditional CNNs.
- Real-world usage: High-end image classification, object detection, and multimodal models (like DALL-E).

## 🧩 Glossary
- [[ViT]] : Vision Transformer. The original architecture by Google.
- [[Patch]] : A small square region of an image (e.g., $16 \times 16$ pixels).
- [[Linear Projection]] : A dense layer used to convert flattened patches into embedding vectors.
- [[Inductive Bias]] : The set of assumptions a model makes about the structure of the data (e.g., CNNs assume local spatial relationships).

## ⚙️ Mechanics (First Principles)
### The ViT Workflow:
1. **Patching:** Divide the image into $N$ non-overlapping patches.
2. **Flattening:** Flatten each patch into a 1D vector (e.g., $16 \times 16 \times 3 = 768$ dimensions).
3. **Linear Projection:** Pass all vectors through a shared Dense layer to create "patch embeddings."
4. **Learnable Tokens:** Add a specialized "Class Token" (like BERT's [CLS]) to the sequence.
5. **Positional Encoding:** Add positional vectors to the embeddings (since the transformer doesn't know the grid positions).
6. **Transformer Encoder:** Process the sequence through standard multi-head attention and MLP blocks.
7. **Classification Head:** Use only the representation of the [CLS] token to predict the final class.

## 📐 Mathematical Foundations
- **Input Transformation:** An image of shape $H \times W \times C$ is converted to a sequence of shape $N \times (P^2 \cdot C)$, where $P$ is patch size and $N = (H \cdot W) / P^2$.

## 💻 Implementation
- High-level ViT architecture in Keras (conceptual):
```python
# Image -> Extract Patches -> Dense(embed_size)
# Add Class Token -> Add Positional Encodings
# For _ in range(N_blocks):
#    MultiHeadAttention -> LayerNorm -> Add
#    MLP -> LayerNorm -> Add
# Dense(n_classes) on [CLS] output
```

## 🧪 Experiments
1. **The Data Hunger Test:** Train a ViT and a ResNet-50 on 10,000 images. Observe that the ResNet wins. Then, train them on 100 million images. Observe that the ViT eventually overtakes the ResNet.

## ⚠️ Constraints & Pitfalls
- [[Data Hunger]] : Because they have no "notion" of 2D space (local connectivity), ViTs need significantly more data to learn visual structures than CNNs.
- **Computation:** Self-attention scales quadratically with the number of patches, limiting the resolution of images that can be processed.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Transformer_Architecture_Fundamentals]]
- Used in → [[Evolution_of_CNN_Architectures]]
- Related to → [[Evolution_of_Large_Language_Models]]
---
(MINIMUM 3 links)
