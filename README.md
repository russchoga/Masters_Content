# LUNG CANCER RESEARCH - Cleopas Russell Choga

**README.md — A Transformer Based Multi-Omics Clinical Decision Support System for Genomic Risk Stratification in Lung Adenocarcinoma**

## Overview
This repository contains the full codebase for a transformer‑based multi‑omics prognostic model for lung adenocarcinoma (LUAD). The work builds directly on the machine‑learning foundation established in my Master’s thesis, where I developed classical and deep learning survival models for LUAD.

To keep pace with modern ML architectures and multi‑omics integration trends, this project extends that thesis by introducing a transformer‑based survival model capable of jointly learning from RNA expression, copy‑number variation (CNV), somatic mutations (MUT), and clinical covariates (CLIN).

The model is trained on TCGA LUAD and externally validated on MSK‑IMPACT LUAD. Because MSK‑IMPACT does not include RNA expression, RNA is excluded only during external validation. All internal training and evaluation use the full multi‑omics feature set.

## Key Features

**Full multi‑omics transformer architecture**
- RNA, CNV, MUT, and CLIN encoders
- Multi‑token fusion
- Transformer encoder layers
- Cox proportional hazards head

**Ablation models**
- RNA‑only
- CNV‑only
- MUT‑only
- CLIN‑only
- CNV+MUT+CLIN (MSK‑compatible)
- Full RNA+CNV+MUT+CLIN (TCGA)
    
**Internal validation (TCGA LUAD)**

**External validation (MSK‑IMPACT LUAD)**
- RNA excluded due to dataset limitations
- IMPACT468 panel filtering
- Primary lung + LUAD filtering
    
**Explainability**
- Attention‑based pathway and gene attribution
- Clinical feature importance
    
**Patient‑level report generation (TCGA)**

## Repository Structure

<img width="726" height="508" alt="image" src="https://github.com/user-attachments/assets/21891665-0531-47aa-93ad-50bc0c33ccbd" />


## Model Summary

**Full Multi‑Omics Transformer (RNA + CNV + MUT + CLIN)**
- RNA: 20k+ genes
- CNV: 25k+ features
- MUT: 19k+ binary mutation indicators
- CLIN: 60 clinical covariates
**Architecture:**
- Linear embeddings → transformer encoder → multi‑omics fusion → Cox head
- Loss: Negative partial log‑likelihood (Cox)
- Output: Risk score (linear predictor)
**MSK‑Compatible Transformer (CNV + MUT + CLIN)**
    Used only for external validation because MSK lacks RNA.
**Clinical‑Only Transformer**
    Used as a generalization baseline.
    
## Datasets

### TCGA LUAD
- Modalities: RNA, CNV, MUT, CLIN
- Endpoint: Overall survival (OS)
- Used for training, internal validation, ablations, explainability
### MSK‑IMPACT LUAD
- Modalities: CNV, MUT, CLIN
- Endpoint: OS
- Used for external validation

### Filters applied:**
1. Primary lung samples
2. LUAD only
3. IMPACT468 panel only
RNA excluded due to dataset limitations

## Results

**Internal (TCGA LUAD)**
- Strong internal discrimination
- Stable calibration
- Clear risk stratification
- Multi‑omics > single‑omics ablations

**External Validation (MSK-IMPACT LUAD)**

| Model | External C‑index |
| --- | --- |
| CNV+MUT+CLIN Transformer | **0.526** |
| Clinical‑Only Transformer | **0.533** |

**Interpretation:**
- Clinical covariates generalize better across cohorts than multi‑omics signals due to cross‑platform genomic differences (TCGA vs MSK).
