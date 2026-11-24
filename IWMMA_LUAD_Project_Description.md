# Auditing SHAP Guidance in Symbolic Rules for Lung Adenocarcinoma Proteomics

**Surajit Das · IWMMA 2026 · Manuscript 20**

## Project description

This project tests whether linear-model SHAP changes the proteins selected, the Horn clauses learned, or the held-out tissue predictions in a proteomics workflow. It combines paired differential proteomics, L1 logistic regression, SHAP attribution, and inductive logic programming. The source is CPTAC-LUAD (PDC000153), with 213 tissues from 111 patients, including 102 tumour–adjacent-normal pairs. The benchmark uses common patient-grouped folds for all methods within each analysis.

Absolute L1 coefficients reproduced the SHAP-guided candidate sets, clauses, and held-out predictions in both analyses. A single-protein threshold reproduced all 204 full-rule predictions in the paired-only analysis. The TMT-channel-only control reached F1 of 0.9911 overall and 0.9903 in paired patients, showing a strong channel–label association and limiting the biological interpretation of the near-ceiling classification scores. The findings apply to this tissue-classification study within CPTAC-LUAD.

## Included files

| Location | Contents |
|---|---|
| `data/` | Three chunks of the raw TMT proteomics matrix, plus the summary table, sample map, and biospecimen manifest |
| `matched/` | Colab notebook, local Python runner, pinned dependencies, and verified common-fold outputs |
| `original/` | Archived notebooks, intermediate files, predictions, and historical outputs |
| `manuscript/` | Revised LaTeX manuscript and all referenced external figures |
| `presentation/` and `submission/` | 30-slide presentation and point-by-point rebuttal |

## Set up the three ZIPs

1. Download `IWMMA_LUAD_Reproducibility_Part_1_of_3.zip`, `IWMMA_LUAD_Reproducibility_Part_2_of_3.zip`, and `IWMMA_LUAD_Reproducibility_Part_3_of_3.zip`.
2. Extract each ZIP into the **same destination folder**. Part 3 contains `START_HERE.txt`, `README.md`, and `assemble_data.py`.
3. Open a terminal in that folder and run `python assemble_data.py` (or `py assemble_data.py` on Windows) using Python 3.11 or later. The script reconstructs the raw matrix and verifies its SHA-256 checksum.

## View or rerun the benchmark

- **View results.** Open `matched/outputs/`. Start with `matched_metrics.csv`, `rule_agreement.csv`, and `channel_only_metrics.csv`. These are the results for the manuscript's common-fold comparison.
- **Run in Colab.** Run `python assemble_data.py --colab` locally. Open `matched/IWMMA_LUAD_Matched_Audit.ipynb` in Colab, run the cells, and upload the generated `IWMMA_LUAD_Colab_Inputs.zip` when prompted. Each download ZIP is under 25 MB. The generated Colab input ZIP can exceed that size.
- **Run locally.** Use Python 3.12. Create and activate a virtual environment, then run the commands below from the extracted project folder.

```bash
python -m pip install -r matched/requirements.txt
python matched/run_matched_audit.py --data-dir data --output-dir luad_rerun
```

The local runner reproduced the bundled matched outputs byte for byte. The analysis cells were also tested locally with the supplied data. The hosted Colab installation and upload steps were not tested.
