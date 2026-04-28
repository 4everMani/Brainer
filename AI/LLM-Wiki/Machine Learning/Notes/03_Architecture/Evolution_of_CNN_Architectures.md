---
id: 03-evol-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Evolution of CNN Architectures

> [!ABSTRACT]
> The performance of computer vision models has advanced rapidly through the ILSVRC ImageNet challenge. From the pioneering LeNet-5 to modern state-of-the-art architectures like SENet and EfficientNet, key innovations have focused on increasing depth, reducing parameter count, and introducing specialized modules like inception units and skip connections.

## 🧠 Intuition First
- Imagine the evolution of building skyscrapers. 
- **LeNet-5 (1998):** A small 5-story building with standard materials. 
- **AlexNet (2012):** A massive skyscraper built by stacking many more floors on top of each other. 
- **GoogLeNet (2014):** A complex building with specialized wings (inception modules) that handle different tasks efficiently. 
- **ResNet (2015):** A building with "express elevators" (skip connections) that allow materials to reach any floor instantly, no matter how tall the building gets.

## 🎯 Why This Matters
- Problem it solves: Provides a roadmap of the most effective architectural patterns for capturing complex hierarchical features in visual data.
- Real-world usage: Selecting the right baseline architecture for custom image recognition tasks.

## 🧩 Glossary
- [[ILSVRC]] : ImageNet Large Scale Visual Recognition Challenge. The premier competition for computer vision.
- [[Top-5 Error Rate]] : The percentage of test images where the correct class is not among the model's top 5 predictions.
- [[LRN]] : Local Response Normalization. A competitive normalization step used in AlexNet (now mostly replaced by Batch Norm).
- [[Bottleneck Layer]] : A $1 \times 1$ convolutional layer used to reduce dimensionality and computational cost.

## ⚙️ Mechanics (First Principles)
### Key Milestone Architectures:
1. **LeNet-5 (LeCun):** Input -> [Conv -> Pool] * 2 -> Dense. Used for digit recognition.
2. **AlexNet (Hinton):** Much deeper/larger. First to stack Convs directly. Used Dropout and Data Augmentation.
3. **GoogLeNet:** Introduced **Inception modules**. Used bottleneck layers to drastically reduce parameter count (6M vs AlexNet's 60M).
4. **ResNet:** Introduced **Skip Connections** to solve the vanishing gradient problem in extremely deep networks (up to 152 layers).
5. **SENet:** Introduced **Squeeze-and-Excitation** blocks to recalibrate feature maps based on channel-wise dependencies.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- High-level progress summary:
| Year | Winner | Innovation | Top-5 Error |
| :--- | :--- | :--- | :--- |
| 1998 | LeNet-5 | Basic Conv/Pool Stack | - |
| 2012 | AlexNet | Deep Stack, Dropout, Augment | 17% |
| 2014 | GoogLeNet | Inception Modules | 6.7% |
| 2015 | ResNet | Skip Connections | 3.6% |
| 2017 | SENet | Feature Map Recalibration | 2.25% |

## 🧪 Experiments
1. **The Parameter Race:** Compare the number of trainable weights in AlexNet vs. GoogLeNet. Observe that GoogLeNet is much deeper but has 10x fewer parameters.

## ⚠️ Constraints & Pitfalls
- **Black Box Nature:** As architectures get deeper and use more complex modules (like Inception or SE blocks), they become harder to interpret and more expensive to train.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Convolutional_Neural_Networks_CNNs]]
- Used in → [[EfficientNet_and_Compound_Scaling]]
- Related to → [[ResNet_and_Residual_Learning]]
---
(MINIMUM 3 links)
