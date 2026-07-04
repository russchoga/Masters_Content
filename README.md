# LUNG CANCER RESEARCH - Cleopas Russell Choga

**README.md — A Transformer Based Multi-Omics Clinical Decision Support System for Genomic Risk Stratification in Lung Adenocarcinoma**

## Overview
This repository contains the full codebase for a transformer‑based multi‑omics prognostic model for lung adenocarcinoma (LUAD). The work builds directly on the machine‑learning foundation established in my Master’s thesis, where I developed classical and deep learning survival models for LUAD.

To keep pace with modern ML architectures and multi‑omics integration trends, this project extends that thesis by introducing a transformer‑based survival model capable of jointly learning from RNA expression, copy‑number variation (CNV), somatic mutations (MUT), and clinical covariates (CLIN).

The model is trained on TCGA LUAD and externally validated on MSK‑IMPACT LUAD. Because MSK‑IMPACT does not include RNA expression, RNA is excluded only during external validation. All internal training and evaluation use the full multi‑omics feature set.

## Key Features

**Full multi‑omics transformer architecture**
1. RNA, CNV, MUT, and CLIN encoders
2. Multi‑token fusion
3. Transformer encoder layers
4. Cox proportional hazards head

**Ablation models**
1. RNA‑only
2. CNV‑only
3. MUT‑only
4. CLIN‑only
5. CNV+MUT+CLIN (MSK‑compatible)
6. Full RNA+CNV+MUT+CLIN (TCGA)
    
**Internal validation (TCGA LUAD)**

**External validation (MSK‑IMPACT LUAD)**
1. RNA excluded due to dataset limitations
2. IMPACT468 panel filtering
3. Primary lung + LUAD filtering
    
**Explainability**
1. Attention‑based pathway and gene attribution
2. Clinical feature importance
    
**Patient‑level report generation (TCGA)**

## Repository Structure

THESIS_LUNG_CANCER_STUDY/
│
├── Write_up/
│   └── Latex/
│       └── transformers/
│           ├── model.py                     # Transformer architectures (RNA, CNV, MUT, CLIN)
│           ├── model_core.py                # Training utilities, loss functions
│           ├── train_luad.py                # TCGA training pipeline (multi-omics + ablations)
│           ├── ext_val_msk_cnv_mut_clin.py  # MSK external validation (RNA excluded)
│           ├── ext_val_msk_clin_only.py     # Clinical-only external validation
│           ├── patient_reports.py           # TCGA patient-level reports
│           └── Data/
│               └── Luad/
│                   ├── luad_transformer_full_multiomics.pt
│                   ├── luad_transformer_cnv_mut_clin.pt
│                   └── luad_transformer_clin_only.pt
│
├── Notebooks/
│   ├── tcga_preprocessing.ipynb
│   ├── msk_preprocessing.ipynb
│   └── explainability.ipynb
│
└── README.md

## Model Summary

**Full Multi‑Omics Transformer (RNA + CNV + MUT + CLIN)**
    -> RNA: 20k+ genes
    -> CNV: 25k+ features
    -> MUT: 19k+ binary mutation indicators
    -> CLIN: 60 clinical covariates
**Architecture:**
    -> Linear embeddings → transformer encoder → multi‑omics fusion → Cox head
    -> Loss: Negative partial log‑likelihood (Cox)
    -> Output: Risk score (linear predictor)
**MSK‑Compatible Transformer (CNV + MUT + CLIN)**
    -> Used only for external validation because MSK lacks RNA.
**Clinical‑Only Transformer**
    -> Used as a generalization baseline.
    
## Datasets

**TCGA LUAD**
  -> Modalities: RNA, CNV, MUT, CLIN
  -> Endpoint: Overall survival (OS)
  -> Used for training, internal validation, ablations, explainability
**MSK‑IMPACT LUAD**
  -> Modalities: CNV, MUT, CLIN
  -> Endpoint: OS
  -> Used for external validation
  -> **Filters applied:**
    -> Primary lung samples
    -> LUAD only
    -> IMPACT468 panel only
  -> RNA excluded due to dataset limitations

## Results

**Internal (TCGA LUAD)**
    -> Strong internal discrimination
    -> Stable calibration
    - Clear risk stratification
    -> Multi‑omics > single‑omics ablations

**External Validation (MSK-IMPACT LUAD)**

| Model | External C‑index |
| --- | --- |
| CNV+MUT+CLIN Transformer | **0.526** |
| Clinical‑Only Transformer | **0.533** |

**Interpretation:**
Clinical covariates generalize better across cohorts than multi‑omics signals due to cross‑platform genomic differences (TCGA vs MSK).
