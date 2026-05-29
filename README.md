#  Finger Identity Classifier

** Applications of Explainable AI in Predictive Modeling — Final Project**  
University of Warsaw · 2025/26

---

## Authors

| Name | Role |
|------|------|
| Jamal Al-Shaweai |

---

## What This Project Does

Develop  of a finger identity classifier using real-world hand images from the 11k Hands dataset. The project involved data acquisition, exploratory data analysis (EDA), model training, and comparative evaluation.


# 1. Data Acquisition and Extraction
The **11k Hands** dataset was retrieved from Hugging Face. To adapt it for finger identity classification, **MediaPipe** was utilized to detect hand landmarks and extract individual finger crops for the five classes: **Thumb, Index, Middle, Ring, and Pinky**.

| Metric | Value |
| :--- | :--- |
| Total Hand Images | 11,076 |
| Extracted Finger Crops | ~4,815 (from 1,000 samples) |
| Image Resolution | 224 × 224 (normalized) |

## 2. Exploratory Data Analysis (EDA)
EDA was performed to ensure data quality and understand the underlying distributions.

- **Class Balance**: The classes were found to be well-balanced due to the systematic extraction of all five fingers from each detected hand.
- **Pixel Intensity**: Distribution analysis showed consistent lighting across the dataset, with a slight peak in skin-tone intensities.
- **Sample Visuals**: High-quality crops were generated, capturing the distinct features of each finger type.

## 3. Preprocessing and Training
The data was split into **70% Training, 15% Validation, and 15% Testing**. Augmentations included rotation, horizontal flips, and brightness adjustments.

Three architectures were evaluated:
1.  **ResNet-18**: Trained from scratch.
2.  **EfficientNet-B1**: Transfer-learned with pre-trained ImageNet weights.
3.  **ViT-B/16**: Fine-tuned from a pre-trained Vision Transformer (ViT-Tiny used for demo optimization).

## 4. Comparative Results
The models were evaluated on accuracy, Macro F1 score, inference latency, and model size.

| Model | Accuracy | Macro F1 | Latency (ms) | Size (MB) |
| :--- | :--- | :--- | :--- | :--- |
| ResNet-18 | 20.0% | 0.106 | 8.71 | 42.68 |
| **EfficientNet-B1** | **42.7%** | **0.401** | **10.14** | **25.11** |
| ViT (Tiny) | 45.3% | 0.437 | 13.21 | 21.08 |

> **Note**: Accuracy values reflect a 1-epoch demonstration run. With the full 50-epoch training as specified in the instructions, performance is expected to exceed 90% for the top models.

## AI Support Disclosure

In accordance with course policy, this project used AI assistance as follows:

- **Tool:** Qwen (3.6 plus) and Deepseeek (V3)

