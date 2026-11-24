# PROTEOMICS2
# Auditing SHAP Guidance in Symbolic Rules for Lung Adenocarcinoma Proteomics

**Surajit Das · IWMMA 2026 · Manuscript 20**

## Overview

This repository contains the data, code, and results for a study of whether SHAP attribution changes the proteins selected, the symbolic rules learned, or the resulting predictions in a lung adenocarcinoma proteomics workflow.

The workflow combines paired differential proteomics, L1 logistic regression, linear-model SHAP, and inductive logic programming. It uses CPTAC-LUAD data from 111 patients, comprising 213 tumour and adjacent-normal tissue samples, including 102 matched pairs. The benchmark evaluates all methods on common patient-grouped folds within each analysis.

## Key findings

- Absolute L1 coefficients reproduced the SHAP-guided candidate sets, Horn clauses, and held-out predictions in both analyses.
- A single-protein threshold reproduced all 204 full-rule predictions in the paired-only analysis.
- A TMT-channel-only control reached F1 of 0.9911 overall and 0.9903 in the paired-only analysis. This strong channel–label association limits the biological interpretation of the high tissue-classification scores.

## Repository contents

| Folder | Contents |
|---|---|
| `data/` | Proteomics data, sample annotations, and biospecimen manifest |
| `matched/` | Colab notebook, local Python runner, pinned dependencies, and verified benchmark outputs |
| `original/` | Archived notebooks, intermediate files, and outputs from the original evaluations |
| `manuscript/` | Revised LaTeX manuscript and figures |
| `presentation/` | 30-slide presentation |
| `submission/` | Point-by-point response to reviewers |

## Getting started

1. Extract all three ZIP files into the **same folder**.
2. From that folder, run `python assemble_data.py` to reconstruct the raw proteomics matrix and verify its SHA-256 checksum. On Windows, you can use `py assemble_data.py`.
3. Open `matched/outputs/` to inspect the verified results. Start with `matched_metrics.csv`, `rule_agreement.csv`, and `channel_only_metrics.csv`.

### Run locally

Use Python 3.12 and run these commands from the project folder in an activated virtual environment.

```bash
python -m pip install -r matched/requirements.txt
python matched/run_matched_audit.py --data-dir data --output-dir luad_rerun
```

### Run in Google Colab

Run `python assemble_data.py --colab` from the project folder. Open `matched/IWMMA_LUAD_Matched_Audit.ipynb` in Colab, run the cells, and upload `IWMMA_LUAD_Colab_Inputs.zip` when prompted.

## Reproducibility

The local runner reproduced the bundled matched outputs byte for byte. The notebook’s analysis cells were tested locally with the supplied data. The hosted Colab installation and upload steps remain untested. Use the outputs in `matched/outputs/` for the manuscript’s common-fold comparisons.
