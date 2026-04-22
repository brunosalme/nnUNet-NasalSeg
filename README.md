# 🫁 Nasal Cavity & Paranasal Sinuses Segmentation with nnU-Net

Automated 3D segmentation of nasal cavity and paranasal sinuses from CT images using **nnU-Net**, a self-configuring deep learning framework. This repository contains the training notebook and dataset configuration generated throughout this project.

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `notebook.ipynb` | Full training pipeline: data prep, nnU-Net setup, training and validation |
| `dataset.json` | Dataset configuration file used for nnU-Net training |

---

## 🧠 About the Task

Segmentation of nasal structures from CT images is a critical step in surgical planning, disease diagnosis, and airflow analysis. This project applies nnU-Net to automatically delineate **5 anatomical structures**:

| Label | Structure |
|-------|-----------|
| 1 | Right Maxillary Sinus |
| 2 | Left Maxillary Sinus |
| 3 | Right Nasal Cavity |
| 4 | Left Nasal Cavity |
| 5 | Nasopharynx |

---

## 📦 Dataset — NasalSeg

Training was performed on the **NasalSeg** dataset, the first large-scale, publicly available annotated dataset for nasal cavity and paranasal sinus segmentation.

- **130** head CT scans (74 male, 56 female; ages 24–82)
- **Pixel-wise manual annotations** for 5 structures
- **5-fold cross-validation** splits provided
- Scanner: Biograph 64 (Siemens); resolution: 0.586 × 0.586 mm; slice spacing: 1.5 mm
- Data available at: [Zenodo — doi:10.5281/zenodo.13893419](https://doi.org/10.5281/zenodo.13893419)

> Zhang, Y. et al. *NasalSeg: A Dataset for Automatic Segmentation of Nasal Cavity and Paranasal Sinuses from 3D CT Images.* Scientific Data 11, 1329 (2024). https://doi.org/10.1038/s41597-024-04176-1

---

## ⚙️ Method — nnU-Net

**nnU-Net** (no-new-Net) is a self-configuring segmentation framework that automatically adapts its entire pipeline — preprocessing, architecture, training, and post-processing — to any new dataset without manual intervention.

Key configurations used:
- **Architecture:** 3D U-Net (encoder–decoder with skip connections)
- **Loss:** Dice + Cross-Entropy
- **Optimizer:** SGD with Nesterov momentum (µ = 0.99)
- **Training:** 1,000 epochs × 250 mini-batches
- **Augmentation:** rotations, scaling, Gaussian noise/blur, brightness, contrast, gamma correction, mirroring

> Isensee, F. et al. *nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation.* Nature Methods 18, 203–211 (2021). https://doi.org/10.1038/s41592-020-01008-z

---

## 🚀 Getting Started

### 1. Install nnU-Net

```bash
pip install nnunetv2
```

### 2. Set environment variables

```bash
export nnUNet_raw="/path/to/nnUNet_raw"
export nnUNet_preprocessed="/path/to/nnUNet_preprocessed"
export nnUNet_results="/path/to/nnUNet_results"
```

### 3. Prepare the dataset

Place data following nnU-Net's folder convention and use the provided `dataset.json`.

### 4. Run training

```bash
nnUNetv2_train DATASET_ID 3d_fullres FOLD
```

### 5. Run inference

```bash
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c 3d_fullres
```

---

## 📊 Baseline Results (NasalSeg — 5-fold cross-validation)

|   Fold   |   DSC (%)  |
|----------|------------|
| Fold 0   |   56.25    |
| Fold 1   |   65.70    |
| Fold 2   |   62.31    |
| Fold 3   |   58.73    |
| Fold 4   |   49.76    |
| **Average** | **58.55** |

*Dice Similarity Coefficient (DSC) reported per fold.*

---

## 📖 References

- Zhang, Y. et al. NasalSeg Dataset — [Zenodo](https://doi.org/10.5281/zenodo.13893419)
- Zhang, Y. et al. NasalSeg Paper — [Scientific Data (2024)](https://doi.org/10.1038/s41597-024-04176-1)
- Isensee, F. et al. nnU-Net — [Nature Methods (2021)](https://doi.org/10.1038/s41592-020-01008-z)
- nnU-Net GitHub — [github.com/MIC-DKFZ/nnUNet](https://github.com/MIC-DKFZ/nnUNet)
- NasalSeg GitHub — [github.com/YichiZhang98/NasalSeg](https://github.com/YichiZhang98/NasalSeg)

---

## 📄 License

This repository is shared for research and educational purposes. Please cite the original NasalSeg and nnU-Net papers if you use this work.
