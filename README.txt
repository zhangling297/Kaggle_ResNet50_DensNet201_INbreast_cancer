INbreast TransUNet Segmentation Project

Run the notebook in Kaggle.
Outputs are generated in /kaggle/working.

Dataset: INbreast (not included)
echo "INbreast TransUNet Segmentation Project" > README.txt

# INBreast Tumor Segmentation & Classification  
**TransUNet + Pixel-level Contrastive Learning + DenseNet**

##  Overview
This project presents an end-to-end deep learning pipeline for **breast tumor analysis** using the INBreast dataset. The workflow integrates:

- **Tumor Segmentation** using TransUNet with pixel-level contrastive learning
- **Density Domain Translation** (C ↔ D) using CycleGAN
- **Tumor Classification** using DenseNet

The goal is to improve robustness across **breast density domains** and enhance tumor detection performance.

---

##  Key Contributions (NEW BIT)
- Introduced **pixel-level contrastive learning** into TransUNet segmentation
- Integrated **domain translation (CycleGAN)** to reduce density shift (C vs D)
- Built a **full pipeline: segmentation → feature learning → classification**
- Addressed **data imbalance and domain generalization**

---

##  Dataset
- **INBreast Dataset** (not included due to license)
- Required structure:
root_dir/
|-Study_id/
| |--image_id.png


CSV format:
- File Name 
- Laterality
- View (CC/MLO)
- ACR (density)
- BI-RADS (label)

---

## ⚙️ Pipeline

### 1. Data Processing
- Filter ACR ∈ {3,4} → Density C/D
- Binary classification:
  - 0 → benign (BI-RADS 1–3)
  - 1 → malignant (BI-RADS ≥4)
- Views: CC and MLO only

---

### 2. Segmentation Model
**Model:** TransUNet  
**Loss:**
- Dice + BCE (segmentation)
- Pixel-level contrastive loss

Loss = Segmentation Loss + lamda * contrastive loss


---

### 3. Domain Adaptation (CycleGAN)
- Learn mapping:
  - C → D
  - D → C
- Improves robustness across breast densities

---

### 4. Classification Model
**Model:** DenseNet  
- Input: segmented tumor regions
- Output: benign vs malignant

---

##  Evaluation Metrics

### Segmentation
- Dice Score
- IoU (Intersection over Union)

### Classification
- Accuracy
- Precision / Recall / F1
- Confusion Matrix

---

##  Results 
| Metric | Value |
|------|------|
| Dice Score | ~0.19 |
| IoU | ~0.07 |

|DenseNet201| Evaluation |
|-------|-------|----- |
| Precision |0.85| 
| Overall Accuracy| 0.78|



---

## Limitations
- Small dataset size
- No pixel-perfect ground truth masks
- Domain shift still challenging
- Contrastive learning requires tuning

---

## How to Run

### 1. Install dependencies

### 2. Train segmentation

### 3. Train CycleGAN using 100 epochs

### 4. Train classifier

---

## 📁 Outputs
Saved in:|kaggle|working|

Includes:
- Model weights (.pth)
- Training logs (.csv)
- Visualization plots

---

##  Reproducibility
- Fixed random seed
- Deterministic splits (by patient recommended)
- Configurable hyperparameters

---

## Author
Ling Zhang
 


---

## License
MIT License
