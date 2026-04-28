---
id: 05-mmap-a1b2
tags: [agentic-ai, 05_Optimization, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Object Detection Metrics mAP

> [!ABSTRACT]
> Mean Average Precision (mAP) is the primary metric for evaluating object detection models. It summarizes the precision-recall trade-off across multiple classes by averaging the maximum precision at various recall levels, while accounting for the spatial accuracy of bounding boxes using Intersection over Union (IoU) thresholds.

## 🧠 Intuition First
- Imagine you're judging an archery contest where some people shoot fast and others take their time. 
- **AP:** Instead of just looking at one shot, you look at the archer's best performance at every possible "speed" (recall). You take the average of these "personal bests." 
- **mAP:** You average the scores across different types of targets (classes). 
- **IoU constraint:** You only count a hit if the arrow lands within a certain distance of the bullseye (e.g., within 5 inches = IoU 0.5).

## 🎯 Why This Matters
- Problem it solves: Provides a single, fair number to compare models that might have different strengths (e.g., one model is very accurate but misses many objects; another finds everything but makes many mistakes).
- Real-world usage: Comparing state-of-the-art models in the COCO and PASCAL VOC competitions.

## 🧩 Glossary
- [[AP]] : Average Precision. The area under the precision-recall curve, often approximated by the mean of maximum precisions at 11 recall levels ($0, 0.1, \dots, 1.0$).
- [[mAP]] : Mean Average Precision. The average of AP scores across all object classes.
- [[IoU Threshold]] : The minimum overlap required to consider a detection as a "True Positive."
- [[mAP@0.5]] : mAP calculated using a fixed IoU threshold of 0.5.
- [[mAP@[.5:.95]]] : The average of mAP scores calculated at 10 different IoU thresholds ($0.5, 0.55, \dots, 0.95$).

## ⚙️ Mechanics (First Principles)
### The Calculation:
1. **Sort:** Rank all detections by their confidence score.
2. **Assign:** For each detection, mark as TP if class is correct and IoU $>$ threshold; else FP.
3. **P-R Curve:** Compute precision and recall at each step in the rank.
4. **Max-Smoothing:** Replace each precision value with the maximum precision to its right on the curve.
5. **Mean:** Calculate the average of these smoothed values to get AP.
6. **Aggregate:** Average APs across all classes to get mAP.

## 📐 Mathematical Foundations
- **IoU Requirement:** $TP \iff (\text{class matches}) \land (IoU(\text{box}_{pred}, \text{box}_{true}) \geq T_{IoU})$.

## 💻 Implementation
- Not applicable (Typically use standard evaluation scripts provided by the dataset, e.g., `pycocotools`).

## 🧪 Experiments
1. **The Threshold Impact:** Calculate the mAP for a model at IoU=0.5 and IoU=0.9. Observe that mAP drops significantly at 0.9 because the model must be almost perfectly placed spatially to count as a success.

## ⚠️ Constraints & Pitfalls
- [[Metric Ambiguity]] : Always specify the IoU threshold when reporting mAP, as mAP@0.5 and mAP@0.75 represent very different performance standards.
- **Redundancy:** The name "Mean Average Precision" is technically redundant but has become the universal standard.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Precision_Recall_Tradeoff]]
- Used in → [[YOLO_Object_Detection]]
- Related to → [[Object_Detection_Mechanics]]
---
(MINIMUM 3 links)
