# Protein abundance modulates the structural localization of continuous-time quantum walks on mitochondrial pathway networks

Analysis code and outputs accompanying the article submitted to *Discover Applied Sciences*.

**Author** Amine Bougarne, Faculty of Medicine and Pharmacy, Mohammed V University, Rabat, Morocco
ORCID [0009-0000-6896-6926](https://orcid.org/0009-0000-6896-6926)

---

## What this repository contains

| Path | Content |
|---|---|
| `CTQW_MitoCarta3_pipeline_v3.ipynb` | Complete analysis pipeline, reference version |
| `CTQW_MitoCarta3_pipeline_KAGGLE.ipynb` | Same pipeline, configured to run on Kaggle with the dataset attached as Input |
| `results/tables/` | 39 CSV tables, every numerical result reported in the article |
| `results/figures/` | 14 figures in PNG and PDF, at 300 dpi |
| `results/session_info.json` | Library versions, random seed, and SHA-256 of the source data |
| `requirements.txt` | Python dependencies |
| `CITATION.cff` | Citation metadata |

## Source data

The pipeline analyses the **Human MitoCarta 3.0** inventory, distributed by the Broad Institute and
described in Rath *et al.*, *Nucleic Acids Research* 49:D1541–D1547 (2021),
<https://doi.org/10.1093/nar/gkaa1011>.

The file is **not redistributed here**. Download `Human_MitoCarta3_0.xls` from
<https://www.broadinstitute.org/mitocarta> and place it beside the notebook.

The exact file analysed has SHA-256 checksum:

```
a885dfb0f2847dc4e3fff2bebb89f47535cf546f2a46ba463016ffa2e5e228b5
```

The notebook verifies and prints this checksum at run time, so any divergence from the version
analysed here is detected immediately.

Note on provenance: the quantitative layer of MitoCarta derives from mass spectrometry of
mitochondria isolated from fourteen **mouse** tissues; human entries are the corresponding
orthologues. The analysis is therefore mammalian, not human.

## How to run

### Locally

```bash
pip install -r requirements.txt
jupyter notebook CTQW_MitoCarta3_pipeline_v3.ipynb
```

`xlrd` is required: the MitoCarta workbook is an Excel 97-2003 (OLE2) file that `openpyxl` cannot read.

### On Kaggle

Attach `Human_MitoCarta3_0.xls` as a dataset under **Input**, then **Run All**. The file is located
automatically. Set `QUICK_RUN = True` for a five-minute structural check; leave it `False` to
reproduce the published numbers.

**Runtime** 60–75 minutes in full mode, dominated by the permutation tests
(5,000 permutations for the primary endpoint, 2,000 for every control and benchmark configuration).
Fixed random seed: 20260805.

## Reproducibility

The pipeline was executed in two independent software environments with different versions of NumPy,
SciPy, pandas and scikit-learn. All primary and robustness results were reproduced identically,
including the fourteen tissue z-scores to two decimal places, the localization decomposition and the
disorder-scaling test. One quantity differed: the AUROC of the classical knockout statistic in one
tissue changed by 0.002, moving the corresponding paired-bootstrap comparison from q = 0.029 to
q = 0.054. Values reported in the article are those produced by the notebooks deposited here.

## Mapping from outputs to the article

| Output | Article |
|---|---|
| `localization_primary.csv` | Table 2, Sect. 3.5 |
| `control_configurations.csv` | Table 4, Sect. 3.7 |
| `localization_decomposition.csv`, `anderson_disorder_scaling.csv` | Fig. 6, Sect. 3.6 |
| `imputation_robustness.csv`, `abundance_scale_robustness.csv`, `observation_window_stability.csv` | Fig. 7, Sect. 3.7 |
| `enrichment_adjusted_logistic.csv`, `enrichment_stratified_permutation.csv` | Table 5, Sect. 3.9 |
| `benchmark_taskA_summary.csv` | Table 6, Sect. 3.10 |
| `benchmark_taskB_performance.csv`, `benchmark_taskB_auroc_deltas.csv` | Table 7, Fig. 9, Sect. 3.10 |
| `lindblad_dt_convergence.csv`, `lindblad_T_convergence.csv` | Sect. 2.4, Sect. 3.11 |
| `detection_depth.csv`, `confound_detection_depth.csv` | Sect. 3.4 |

## A note on the disease-gene list

The list of mitochondrial disease-associated proteins used in Sect. 3.9 is a curated working list
assembled from clinical-genetics reviews and public catalogues, not a versioned database export. It is
provided in full as `results/tables/knockout_scan_with_exposure.csv` and as Online Resource 4 of the
article, so that replication against a dated MITOMAP or OMIM release is straightforward.

## How to cite

Bougarne A. *Analysis pipeline for "Protein abundance modulates the structural localization of
continuous-time quantum walks on mitochondrial pathway networks"*. Version 3.0.0. Zenodo; 2026.
DOI: [10.5281/zenodo.23534595](https://doi.org/10.5281/zenodo.23534595)

This archive is the version of record for the code; the article itself should be cited separately
once published.

## Licence

Code and derived tables are released under the MIT Licence (see `LICENSE`). The MitoCarta 3.0 source
data remain subject to the terms of the Broad Institute.
