# 🧬 Weakly Supervised Cell-Level Protein Localization  
**Attention-Based MIL with Pseudo-Label Refinement (HPA Dataset)**

This repository implements a multi-stage weakly supervised learning pipeline to predict **protein subcellular localization at the single-cell level** using only **image-level labels** from the Human Protein Atlas (HPA) dataset.  
The framework combines **cell segmentation**, **weak supervision**, **attention-based Multiple Instance Learning (MIL)**, and **pseudo-label refinement** to learn meaningful cell representations without any ground-truth cell annotations.

---

## 📌 Motivation

In the HPA dataset, each microscopy image contains many heterogeneous cells, but labels are provided only at the image level.  
Assigning the same label to every cell introduces heavy noise and makes standard supervised learning unreliable.

This project addresses the problem by:
- Segmenting individual cells
- Learning cell-level embeddings under weak supervision
- Using attention to identify informative cells
- Refining noisy labels via pseudo-labeling and threshold calibration

---

## 📁 Repository Structure

.
├── 1_cell_segmentation.ipynb
├── 2_weakly_supervised_cell_training.ipynb
├── 3_attention_mil_training.ipynb
├── 4_pseudo_label_refinement.ipynb
├── data/
│   └── .gitkeep
├── outputs/
│   ├── cell_crops/
│   ├── embeddings/
│   ├── attention_maps/
│   └── metrics/
└── README.md


