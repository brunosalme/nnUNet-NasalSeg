# 🫁 Nasal Cavity & Paranasal Sinuses Segmentation with nnU-Net

> **Bringing state-of-the-art deep learning segmentation to researchers and clinicians — free, open, and ready to use in 3D Slicer.**

Automated 3D segmentation of nasal cavity and paranasal sinuses from CT images using **nnU-Net**. This repository provides trained model weights and configuration files so that **anyone with a CT scan and 3D Slicer can run automatic segmentation — no coding required.**

---

## 🎯 Mission

Advanced medical image segmentation is often locked behind expensive commercial software or requires deep technical expertise. This project challenges that reality.

By publishing our trained nnU-Net models as open artifacts, we aim to give **researchers, surgeons, and students** direct access to automatic CT segmentation of nasal structures — using only free, open-source tools. If you have a CT scan and a computer, you have everything you need.

---

## ✅ What You Can Do With This

- **Automatically segment** nasal cavity and paranasal sinuses from any head CT
- **Use 3D Slicer** (free software) to load, run, and visualize results — no coding required
- **Reproduce or extend** the training using the provided notebook and `dataset.json`
- **Integrate into clinical or research workflows** at zero software cost

---

## 🗂️ Repository Contents

| File | Description |
|------|-------------|
| `notebook.ipynb` | Full training pipeline: data prep, nnU-Net setup, training and validation |
| `dataset.json` | Dataset configuration file used for nnU-Net training |
| `model/` | Trained nnU-Net weights (ready for inference) |

---

## 🖥️ Running Segmentation in 3D Slicer (No Coding Required)

[3D Slicer](https://www.slicer.org/) is a free, open-source platform for medical image analysis. With the **SlicernnUNet** extension, you can run our trained model directly on your CT scans.

### Step 1 — Install 3D Slicer
Download and install from [slicer.org](https://www.slicer.org/) (Windows, macOS, Linux).

### Step 2 — Install the MONAILabel or nnU-Net extension
In 3D Slicer, go to **Extensions Manager** and install **MONAILabel** or a compatible nnU-Net inference extension.

### Step 3 — Load your CT
Open your CT scan via **File > Add Data**.

### Step 4 — Run inference
Point the extension to the model weights from this repository and run automatic segmentation. The 5 nasal structures will be labeled and rendered in 3D.

### Step 5 — Review and export
Inspect, correct, and export the segmentation masks for your workflow (NRRD, NIfTI, STL for 3D printing, etc.).

> 💡 **Tip:** 3D Slicer's **Segment Editor** allows manual correction of any predicted labels after inference.

---

## 🧠 Segmentation Targets

The model delineates **5 anatomical structures**:

| Label | Structure |
|-------|-----------|
| 1 | Right Maxillary Sinus |
| 2 | Left Maxillary Sinus |
| 3 | Right Nasal Cavity |
| 4 | Left Nasal Cavity |
| 5 | Nasopharynx |

---

## 📦 Dataset — NasalSeg

Training was performed on the **NasalSeg** dataset — the first large-scale, publicly available annotated dataset for nasal cavity and paranasal sinus segmentation.

- **130** head CT scans (74 male, 56 female; ages 24–82)
- **Pixel-wise manual annotations** for 5 structures
- **5-fold cross-validation** splits
- Scanner: Biograph 64 (Siemens); in-plane resolution: 0.586 × 0.586 mm; slice spacing: 1.5 mm
- Data: [Zenodo — doi:10.5281/zenodo.13893419](https://doi.org/10.5281/zenodo.13893419)

> Zhang, Y. et al. *NasalSeg: A Dataset for Automatic Segmentation of Nasal Cavity and Paranasal Sinuses from 3D CT Images.* Scientific Data 11, 1329 (2024). https://doi.org/10.1038/s41597-024-04176-1

---

## ⚙️ Method — nnU-Net

**nnU-Net** is a self-configuring segmentation framework that automatically adapts its entire pipeline — preprocessing, network architecture, training, and post-processing — to any new dataset, without manual intervention.

Key training configuration:

| Parameter | Value |
|-----------|-------|
| Architecture | 3D U-Net (encoder–decoder + skip connections) |
| Loss | Dice + Cross-Entropy |
| Optimizer | SGD, Nesterov momentum µ = 0.99 |
| Training | 1,000 epochs × 250 mini-batches |
| Augmentation | Rotations, scaling, Gaussian noise/blur, brightness, contrast, gamma, mirroring |

> Isensee, F. et al. *nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation.* Nature Methods 18, 203–211 (2021). https://doi.org/10.1038/s41592-020-01008-z

---

## 📊 Baseline Results (5-fold cross-validation)

| Fold | DSC (%) |
|------|---------|
| Fold 0 | 56.25 |
| Fold 1 | 65.70 |
| Fold 2 | 62.31 |
| Fold 3 | 58.73 |
| Fold 4 | 49.76 |
| **Average** | **58.55** |

*Dice Similarity Coefficient (DSC). Results from the NasalSeg benchmark.*

---

## 🔬 For Developers — Reproduce or Retrain

<details>
<summary>Click to expand</summary>

### Install nnU-Net

```bash
pip install nnunetv2
```

### Set environment variables

```bash
export nnUNet_raw="/path/to/nnUNet_raw"
export nnUNet_preprocessed="/path/to/nnUNet_preprocessed"
export nnUNet_results="/path/to/nnUNet_results"
```

### Prepare the dataset

Follow [nnU-Net's data format](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format.md) and use the provided `dataset.json`.

### Train

```bash
nnUNetv2_train DATASET_ID 3d_fullres FOLD
```

### Predict

```bash
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c 3d_fullres
```

</details>

---

## 📖 References

- Zhang, Y. et al. NasalSeg Dataset — [Zenodo](https://doi.org/10.5281/zenodo.13893419)
- Zhang, Y. et al. NasalSeg Paper — [Scientific Data (2024)](https://doi.org/10.1038/s41597-024-04176-1)
- Isensee, F. et al. nnU-Net — [Nature Methods (2021)](https://doi.org/10.1038/s41592-020-01008-z)
- nnU-Net GitHub — [github.com/MIC-DKFZ/nnUNet](https://github.com/MIC-DKFZ/nnUNet)
- NasalSeg GitHub — [github.com/YichiZhang98/NasalSeg](https://github.com/YichiZhang98/NasalSeg)
- 3D Slicer — [slicer.org](https://www.slicer.org/)

---

## 📄 License

This repository is shared openly for research and educational purposes. Please cite the original NasalSeg and nnU-Net papers if you use this work in your research.

---

*Making advanced medical image segmentation accessible — one CT at a time.*
