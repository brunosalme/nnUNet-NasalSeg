
<div align="center">

# 🫁 Nasal Cavity & Paranasal Sinuses Segmentation with nnU-Net

**🌐 Language / Idioma:**
[🇺🇸 English](#english) · [🇧🇷 Português](#português)

</div>

---

<a name="english"></a>

## 🇺🇸 English

> **Bringing state-of-the-art deep learning segmentation to researchers and clinicians — free, open, and ready to use in 3D Slicer.**

Automated 3D segmentation of nasal cavity and paranasal sinuses from CT images using **nnU-Net**. This repository provides trained model weights and configuration files so that **anyone with a CT scan and 3D Slicer can run automatic segmentation — no coding required.**

### 👩‍🔬 About This Research

This repository is the result of research conducted by **SÁ BARRETO, Natália**, within the **Graduate Program in Dentistry (PPGO)** at the **Universidade Federal do Ceará (UFC)**, Brazil.

The work aims to make cutting-edge automatic CT segmentation technology accessible to researchers and health professionals at low cost, using only free and open-source tools.

### 🎯 Mission

Advanced medical image segmentation is often locked behind expensive commercial software or requires deep technical expertise. This project challenges that reality.

By publishing our trained nnU-Net models as open artifacts, we aim to give **researchers, surgeons, and students** direct access to automatic CT segmentation of nasal structures — using only free, open-source tools. If you have a CT scan and a computer, you have everything you need.

### ✅ What You Can Do With This

- **Automatically segment** nasal cavity and paranasal sinuses from any head CT
- **Use 3D Slicer** (free software) to load, run, and visualize results — no coding required
- **Reproduce or extend** the training using the provided notebook and `dataset.json`
- **Integrate into clinical or research workflows** at zero software cost

### 🗂️ Repository Contents

| File | Description |
|------|-------------|
| `notebook.ipynb` | Full training pipeline: data prep, nnU-Net setup, training and validation |
| `dataset.json` | Dataset configuration file used for nnU-Net training |
| `model/` | Trained nnU-Net weights (ready for inference) |

### 🖥️ Running Segmentation in 3D Slicer (No Coding Required)

[3D Slicer](https://www.slicer.org/) is a free, open-source platform for medical image analysis. With the **MONAILabel** or **nnU-Net** extension, you can run our trained model directly on your CT scans.

**Step 1 — Install 3D Slicer**
Download and install from [slicer.org](https://www.slicer.org/) (Windows, macOS, Linux).

**Step 2 — Install the MONAILabel or nnU-Net extension**
In 3D Slicer, go to **Extensions Manager** and install **MONAILabel** or a compatible nnU-Net inference extension.

**Step 3 — Load your CT**
Open your CT scan via **File > Add Data**.

**Step 4 — Run inference**
Point the extension to the model weights from this repository and run automatic segmentation. The 5 nasal structures will be labeled and rendered in 3D.

**Step 5 — Review and export**
Inspect, correct, and export the segmentation masks for your workflow (NRRD, NIfTI, STL for 3D printing, etc.).

> 💡 **Tip:** 3D Slicer's **Segment Editor** allows manual correction of any predicted labels after inference.

### 🧠 Segmentation Targets

| Label | Structure |
|-------|-----------|
| 1 | Right Maxillary Sinus |
| 2 | Left Maxillary Sinus |
| 3 | Right Nasal Cavity |
| 4 | Left Nasal Cavity |
| 5 | Nasopharynx |

### 📦 Dataset — NasalSeg

Training was performed on the **NasalSeg** dataset — the first large-scale, publicly available annotated dataset for nasal cavity and paranasal sinus segmentation.

- **130** head CT scans (74 male, 56 female; ages 24–82)
- **Pixel-wise manual annotations** for 5 structures
- **5-fold cross-validation** splits
- Scanner: Biograph 64 (Siemens); resolution: 0.586 × 0.586 mm; slice spacing: 1.5 mm
- Data: [Zenodo — doi:10.5281/zenodo.13893419](https://doi.org/10.5281/zenodo.13893419)

> Zhang, Y. et al. *NasalSeg: A Dataset for Automatic Segmentation of Nasal Cavity and Paranasal Sinuses from 3D CT Images.* Scientific Data 11, 1329 (2024). https://doi.org/10.1038/s41597-024-04176-1

### ⚙️ Method — nnU-Net

**nnU-Net** is a self-configuring segmentation framework that automatically adapts its entire pipeline to any new dataset, without manual intervention.

| Parameter | Value |
|-----------|-------|
| Architecture | 3D U-Net (encoder–decoder + skip connections) |
| Loss | Dice + Cross-Entropy |
| Optimizer | SGD, Nesterov momentum µ = 0.99 |
| Training | 1,000 epochs × 250 mini-batches |
| Augmentation | Rotations, scaling, Gaussian noise/blur, brightness, contrast, gamma, mirroring |

> Isensee, F. et al. *nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation.* Nature Methods 18, 203–211 (2021). https://doi.org/10.1038/s41592-020-01008-z

### 📊 Results (5-fold cross-validation)

| Fold | DSC (%) |
|------|---------|
| Fold 0 | 56.25 |
| Fold 1 | 65.70 |
| Fold 2 | 62.31 |
| Fold 3 | 58.73 |
| Fold 4 | 49.76 |
| **Average** | **58.55** |

### 🔬 For Developers — Reproduce or Retrain

<details>
<summary>Click to expand</summary>

```bash
pip install nnunetv2

export nnUNet_raw="/path/to/nnUNet_raw"
export nnUNet_preprocessed="/path/to/nnUNet_preprocessed"
export nnUNet_results="/path/to/nnUNet_results"

# Train
nnUNetv2_train DATASET_ID 3d_fullres FOLD

# Predict
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c 3d_fullres
```

</details>

### 📖 References

- Zhang, Y. et al. NasalSeg Dataset — [Zenodo](https://doi.org/10.5281/zenodo.13893419)
- Zhang, Y. et al. NasalSeg Paper — [Scientific Data (2024)](https://doi.org/10.1038/s41597-024-04176-1)
- Isensee, F. et al. nnU-Net — [Nature Methods (2021)](https://doi.org/10.1038/s41592-020-01008-z)
- nnU-Net GitHub — [github.com/MIC-DKFZ/nnUNet](https://github.com/MIC-DKFZ/nnUNet)
- NasalSeg GitHub — [github.com/YichiZhang98/NasalSeg](https://github.com/YichiZhang98/NasalSeg)
- 3D Slicer — [slicer.org](https://www.slicer.org/)

### 📄 License

This repository is shared openly for research and educational purposes. Please cite the original NasalSeg and nnU-Net papers if you use this work.

*Making advanced medical image segmentation accessible — one CT at a time.*

---
---

<a name="português"></a>

## 🇧🇷 Português

> **Levando segmentação por deep learning de última geração a pesquisadores e clínicos — gratuito, aberto e pronto para usar no 3D Slicer.**

Segmentação 3D automatizada de cavidade nasal e seios paranasais a partir de imagens de TC usando **nnU-Net**. Este repositório disponibiliza pesos do modelo treinado e arquivos de configuração para que **qualquer pessoa com uma TC e o 3D Slicer possa realizar segmentação automática — sem necessidade de programação.**

### 👩‍🔬 Sobre Esta Pesquisa

Este repositório é fruto da pesquisa de **SÁ BARRETO, Natália**, junto ao **Programa de Pós-Graduação em Odontologia (PPGO)** da **Universidade Federal do Ceará (UFC)**, Brasil.

O trabalho tem como objetivo tornar a tecnologia de segmentação automática de TC de última geração acessível a pesquisadores e profissionais de saúde a baixo custo, utilizando apenas ferramentas gratuitas e de código aberto.

### 🎯 Missão

A segmentação avançada de imagens médicas frequentemente está restrita a softwares comerciais caros ou exige profundo conhecimento técnico. Este projeto desafia essa realidade.

Ao publicar os modelos nnU-Net treinados como artefatos abertos, buscamos oferecer a **pesquisadores, cirurgiões e estudantes** acesso direto à segmentação automática de estruturas nasais em TC — usando apenas ferramentas gratuitas e de código aberto. Se você tem uma TC e um computador, tem tudo o que precisa.

### ✅ O Que Você Pode Fazer Com Isso

- **Segmentar automaticamente** cavidade nasal e seios paranasais em qualquer TC de crânio
- **Usar o 3D Slicer** (software gratuito) para carregar, executar e visualizar os resultados — sem programação
- **Reproduzir ou estender** o treinamento usando o notebook e o `dataset.json` fornecidos
- **Integrar em fluxos de trabalho clínicos ou de pesquisa** sem custo de software

### 🗂️ Conteúdo do Repositório

| Arquivo | Descrição |
|---------|-----------|
| `notebook.ipynb` | Pipeline completo de treinamento: preparação de dados, configuração do nnU-Net, treinamento e validação |
| `dataset.json` | Arquivo de configuração do dataset utilizado no treinamento do nnU-Net |
| `model/` | Pesos do modelo nnU-Net treinado (prontos para inferência) |

### 🖥️ Executando a Segmentação no 3D Slicer (Sem Programação)

O [3D Slicer](https://www.slicer.org/) é uma plataforma gratuita e de código aberto para análise de imagens médicas. Com a extensão **MONAILabel** ou **nnU-Net**, você pode executar nosso modelo treinado diretamente nas suas TCs.

**Passo 1 — Instale o 3D Slicer**
Baixe e instale em [slicer.org](https://www.slicer.org/) (Windows, macOS, Linux).

**Passo 2 — Instale a extensão MONAILabel ou nnU-Net**
No 3D Slicer, acesse o **Extensions Manager** e instale o **MONAILabel** ou uma extensão compatível com inferência nnU-Net.

**Passo 3 — Carregue sua TC**
Abra sua TC em **File > Add Data**.

**Passo 4 — Execute a inferência**
Aponte a extensão para os pesos do modelo deste repositório e execute a segmentação automática. As 5 estruturas nasais serão rotuladas e renderizadas em 3D.

**Passo 5 — Revise e exporte**
Inspecione, corrija e exporte as máscaras de segmentação conforme seu fluxo de trabalho (NRRD, NIfTI, STL para impressão 3D, etc.).

> 💡 **Dica:** O **Segment Editor** do 3D Slicer permite a correção manual de qualquer rótulo predito após a inferência.

### 🧠 Estruturas Segmentadas

| Rótulo | Estrutura |
|--------|-----------|
| 1 | Seio Maxilar Direito |
| 2 | Seio Maxilar Esquerdo |
| 3 | Cavidade Nasal Direita |
| 4 | Cavidade Nasal Esquerda |
| 5 | Nasofaringe |

### 📦 Dataset — NasalSeg

O treinamento foi realizado com o dataset **NasalSeg** — o primeiro dataset público de grande escala com anotações para segmentação de cavidade nasal e seios paranasais.

- **130** TCs de crânio (74 homens, 56 mulheres; idades 24–82 anos)
- **Anotações manuais pixel a pixel** para 5 estruturas
- Divisões para **validação cruzada em 5 folds**
- Scanner: Biograph 64 (Siemens); resolução: 0,586 × 0,586 mm; espaçamento entre cortes: 1,5 mm
- Dados disponíveis em: [Zenodo — doi:10.5281/zenodo.13893419](https://doi.org/10.5281/zenodo.13893419)

> Zhang, Y. et al. *NasalSeg: A Dataset for Automatic Segmentation of Nasal Cavity and Paranasal Sinuses from 3D CT Images.* Scientific Data 11, 1329 (2024). https://doi.org/10.1038/s41597-024-04176-1

### ⚙️ Método — nnU-Net

O **nnU-Net** é um framework de segmentação auto-configurável que adapta automaticamente todo o pipeline — pré-processamento, arquitetura, treinamento e pós-processamento — a qualquer novo dataset, sem intervenção manual.

| Parâmetro | Valor |
|-----------|-------|
| Arquitetura | 3D U-Net (encoder–decoder + skip connections) |
| Função de perda | Dice + Cross-Entropy |
| Otimizador | SGD, momento de Nesterov µ = 0,99 |
| Treinamento | 1.000 épocas × 250 mini-batches |
| Augmentação | Rotações, escala, ruído/blur gaussiano, brilho, contraste, gamma, espelhamento |

> Isensee, F. et al. *nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation.* Nature Methods 18, 203–211 (2021). https://doi.org/10.1038/s41592-020-01008-z

### 📊 Resultados (validação cruzada em 5 folds)

| Fold | DSC (%) |
|------|---------|
| Fold 0 | 56,25 |
| Fold 1 | 65,70 |
| Fold 2 | 62,31 |
| Fold 3 | 58,73 |
| Fold 4 | 49,76 |
| **Média** | **58,55** |

### 🔬 Para Desenvolvedores — Reproduzir ou Retreinar

<details>
<summary>Clique para expandir</summary>

```bash
pip install nnunetv2

export nnUNet_raw="/caminho/para/nnUNet_raw"
export nnUNet_preprocessed="/caminho/para/nnUNet_preprocessed"
export nnUNet_results="/caminho/para/nnUNet_results"

# Treinar
nnUNetv2_train DATASET_ID 3d_fullres FOLD

# Predizer
nnUNetv2_predict -i PASTA_ENTRADA -o PASTA_SAIDA -d DATASET_ID -c 3d_fullres
```

</details>

### 📖 Referências

- Zhang, Y. et al. NasalSeg Dataset — [Zenodo](https://doi.org/10.5281/zenodo.13893419)
- Zhang, Y. et al. NasalSeg Paper — [Scientific Data (2024)](https://doi.org/10.1038/s41597-024-04176-1)
- Isensee, F. et al. nnU-Net — [Nature Methods (2021)](https://doi.org/10.1038/s41592-020-01008-z)
- nnU-Net GitHub — [github.com/MIC-DKFZ/nnUNet](https://github.com/MIC-DKFZ/nnUNet)
- NasalSeg GitHub — [github.com/YichiZhang98/NasalSeg](https://github.com/YichiZhang98/NasalSeg)
- 3D Slicer — [slicer.org](https://www.slicer.org/)

### 📄 Licença

Este repositório é compartilhado abertamente para fins de pesquisa e educação. Por favor, cite os artigos originais do NasalSeg e do nnU-Net caso utilize este trabalho em suas pesquisas.

*Tornando a segmentação avançada de imagens médicas acessível — uma TC de cada vez.*
