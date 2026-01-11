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



---

## 📓 Notebook Description

### 1️⃣ `1_cell_segmentation.ipynb`
- Uses **Cellpose + Segment Anything (SAM)**  
- Segments multi-cell microscopy images into single-cell instances  
- Extracts 4-channel crops:
  - Green → Protein of interest  
  - Blue → Nucleus (DAPI)  
  - Red → Microtubules  
  - Yellow → Golgi / ER  
- Converts each image into a bag of cell instances  

---

### 2️⃣ `2_weakly_supervised_cell_training.ipynb`
- Trains a **4-channel ResNet-50** backbone  
- Each cell inherits its parent image labels (weak supervision)  
- Multi-label training using:
  - Sigmoid activation  
  - Binary Cross-Entropy loss  
- Produces cell-level embeddings  

---

### 3️⃣ `3_attention_mil_training.ipynb`
- Implements **Attention-Based Multiple Instance Learning (MIL)**  
- Treats each image as a bag of cell embeddings  
- Learns to assign importance weights to individual cells  
- Improves robustness against label noise  
- Produces attention maps for interpretability  

---

### 4️⃣ `4_pseudo_label_refinement.ipynb`
- Introduces a **pseudo-label refinement loop**
- Combines:
  - MIL attention scores  
  - Prediction confidence  
  - Per-class threshold tuning  
- Selects high-confidence cells  
- Retrains:
  - Cell-level backbone  
  - MIL model  
- Improves representation stability and calibration  

---

## 🧠 Core Techniques

- Weakly Supervised Learning  
- Attention-Based Multiple Instance Learning (MIL)  
- Pseudo-Label Refinement  
- Cellpose + SAM Segmentation  
- Multi-label Classification  
- Per-Class Threshold Calibration  
- Handling Extreme Class Imbalance  

---

## 📊 Key Insights

- Attention is more reliable than weak labels for identifying informative cells  
- Pseudo-label refinement improves representation quality and interpretability  
- Threshold tuning has a stronger impact than architectural changes under imbalance  
- Weak supervision exhibits a natural performance ceiling  

---

## 🧪 Dataset

### 🔗 Human Protein Atlas (HPA)

- Kaggle Challenge:  
  https://www.kaggle.com/competitions/human-protein-atlas-image-classification  

- Official Website:  
  https://www.proteinatlas.org  

Dataset characteristics:
- 4-channel fluorescence microscopy images  
- 19 subcellular localization classes  
- Multi-label and highly imbalanced  
- Only image-level annotations provided  

Channels:
| Channel | Meaning |
|-------|-------|
| Green | Protein of interest |
| Blue | Nucleus (DAPI) |
| Red | Microtubules |
| Yellow | Golgi / Endoplasmic Reticulum |

---

## ⚙️ Installation

```bash
pip install torch torchvision opencv-python cellpose numpy pandas scikit-learn matplotlib tqdm
## ✨ Project Highlights

- End-to-end weakly supervised pipeline  
- No cell-level annotations required  
- Attention acts as an implicit denoising mechanism  
- Pseudo-labeling improves calibration and interpretability  
- Transferable to other microscopy tasks such as:
  - Rare-cell detection  
  - Disease phenotyping  
  - Spatial transcriptomics  

---

## 📚 References

- HPA Kaggle Challenge:  
  https://www.kaggle.com/competitions/human-protein-atlas-image-classification  

- Ilse et al., *Attention-based Deep Multiple Instance Learning*, ICML 2018  

- Cellpose-SAM:  
  https://www.biorxiv.org/content/10.1101/2025.04.28.651001v1  


