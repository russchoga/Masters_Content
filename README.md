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

<img width="726" height="508" alt="image" src="https://github.com/user-attachments/assets/21891665-0531-47aa-93ad-50bc0c33ccbd" />


## Model Summary

**Full Multi‑Omics Transformer (RNA + CNV + MUT + CLIN)**
1. RNA: 20k+ genes
2. CNV: 25k+ features
3. MUT: 19k+ binary mutation indicators
4. CLIN: 60 clinical covariates
**Architecture:**
1. Linear embeddings → transformer encoder → multi‑omics fusion → Cox head
2. Loss: Negative partial log‑likelihood (Cox)
3. Output: Risk score (linear predictor)
**MSK‑Compatible Transformer (CNV + MUT + CLIN)**
    Used only for external validation because MSK lacks RNA.
**Clinical‑Only Transformer**
    Used as a generalization baseline.
    
## Datasets

**TCGA LUAD**
1. Modalities: RNA, CNV, MUT, CLIN
2. Endpoint: Overall survival (OS)
3. Used for training, internal validation, ablations, explainability
**MSK‑IMPACT LUAD**
1. Modalities: CNV, MUT, CLIN
2. Endpoint: OS
3. Used for external validation
    a.  **Filters applied:**
    b. Primary lung samples
    c. LUAD only
    d. IMPACT468 panel only
   RNA excluded due to dataset limitations

## Results

**Internal (TCGA LUAD)**
    Strong internal discrimination
    table calibration
    Clear risk stratification
    Multi‑omics > single‑omics ablations

**External Validation (MSK-IMPACT LUAD)**

| Model | External C‑index |
| --- | --- |
| CNV+MUT+CLIN Transformer | **0.526** |
| Clinical‑Only Transformer | **0.533** |

**Interpretation:**
Clinical covariates generalize better across cohorts than multi‑omics signals due to cross‑platform genomic differences (TCGA vs MSK).
