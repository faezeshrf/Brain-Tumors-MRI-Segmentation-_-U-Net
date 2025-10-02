# Brain-Tumors-MRI-Segmentation | U-Net Architecture

# 🧠 Brain Tumor Segmentation (BraTS20, U-Net with Keras/TensorFlow)

## 📌 Project Overview
This repository contains my work on **brain tumor segmentation** using the [BraTS2020 dataset](https://www.med.upenn.edu/cbica/brats2020/).  
The model is based on a **U-Net architecture** implemented in TensorFlow/Keras, trained on multimodal MRI scans (FLAIR, T1ce, etc.).  



---

## 🗂 Dataset
- Dataset: **BraTS20 Training + Validation set** (via KaggleHub/Colab integration)  
- Modalities used (per subject):
  - **FLAIR** (fluid attenuated inversion recovery)  
  - **T1ce** (post-contrast T1-weighted)  
  - **Segmentation mask** (labels: background, tumor core, edema, enhancing tumor)  
- Each subject contains NIfTI files (`.nii.gz`).

---

## ⚙️ Preprocessing
- **Normalization:** Percentile-based robust normalization (1st–99th percentile).  
- **Resizing:** 2D slices resized to `(128 × 128)`.  
- **Label adjustment:** Label `4` (non-enhancing tumor) mapped to `3` for consistency.  
- **One-hot encoding** of segmentation masks.  

---

##  Data Generator
A custom `DataGenerator` was implemented for:
- Efficient loading of `.nii.gz` volumes  
- Multi-channel input (currently tested with **2 channels: FLAIR + T1ce**)  
- Flexible extension to 4 channels (adding T1 and T2)  
- On-the-fly batching, shuffling, and augmentation options  

---

##  Model
- **Architecture:** Batch-normalized U-Net (`build_unet_bn_full`)  
- **Input shape:** `(128, 128, n_channels)`  
- **Output:** `(128, 128, 4)` segmentation masks  

---

##  Loss & Metrics
- Loss function: **CE + Dice Loss (combined)**  
- Metrics monitored:
  - **Dice coefficient (macro & class-wise)**
  - **IoU (macro & per class)**
  - **Precision / Recall / Specificity** (per class)  

---

## Current Status
- ✅ Dataset download & verification  
- ✅ Preprocessing pipeline implemented  
- ✅ Data generator (2–4 channel support)  
- ✅ Model definition (U-Net with BN)  
- ✅ Losses & metrics defined  
- ✅ Training loop started (Colab limited runtime)  



---



---

##  Next Steps
1. **Resume full training** (with GPU/TPU or local HPC cluster)  
2. **Experiment with 4-channel input** (FLAIR, T1, T1ce, T2)  
3. **Add data augmentation** (rotation, flipping, elastic deformation)  
4. **Evaluate performance** on validation & test sets (Dice, IoU)  
5. **Visualize segmentation results** with overlay plots  
6. **Hyperparameter tuning** (learning rate, batch size, optimizer)  
7. **Future extensions**:
   - 3D U-Net  
   - Attention U-Net  
   - Post-processing with CRFs  

---


