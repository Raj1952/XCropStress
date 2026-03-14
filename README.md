# XCropStress

**Explainable Multi-Class Crop Stress Detection using SHAP Feature Attribution on Sentinel-2 Spectral Indices**

> Research paper: *XCropStress: A Controlled Simulation Study for Explainable Multi-Class Crop Stress Detection Using SHAP Feature Attribution on Sentinel-2 Spectral Indices*
> Rajvardhan Ajitrao Jagtap, Sarang Santosh Lavhate 

---

## What this is

XCropStress is a controlled simulation framework that trains a Random Forest classifier on synthetic Sentinel-2 spectral indices and uses SHAP TreeExplainer to produce per-class feature importance rankings across four crop stress types:

- Drought
- Pest / Disease
- Nutrient Deficiency
- Heat Stress

The dataset (4,800 parcels, 1,200 per class) is generated parametrically using means and variances from three peer-reviewed 2025 publications on Sentinel-2 remote sensing in India — no raw satellite imagery required.

**Key result:** NDWI temporal rate-of-change ranks 7.8× more important than NDVI mean in overall SHAP attribution. All three NDVI-derived features rank in the bottom three of ten. This contradicts the conventional reliance on NDVI as the primary crop stress indicator.

---

## Results summary

| Model | Accuracy | F1-Score | Cohen's Kappa |
|---|---|---|---|
| SVM Baseline | 79.38% | 79.31% | — |
| Decision Tree | 83.23% | 83.18% | — |
| Random Forest (standalone) | 88.75% | 88.62% | — |
| **XCropStress RF + SHAP** | **91.15%** | **91.06%** | **0.8819** |

5-fold cross-validation F1: **92.17% ± 0.53%**

---

## Features used

10 spectral features derived from Sentinel-2 bands:

| Feature | Description |
|---|---|
| `NDVI_mean` | Chlorophyll-driven canopy vigor |
| `NDWI_mean` | Canopy water content |
| `EVI_mean` | Background-corrected canopy vigor |
| `LAI_mean` | Leaf Area Index (canopy structure) |
| `NDWI_rate_of_change` | Temporal NDWI trajectory (6 composites) |
| `LAI_temporal_mean` | LAI trajectory mean |
| `LAI_std_dev` | Canopy structural irregularity |
| `EVI_temporal_mean` | EVI trajectory mean |
| `NDVI_rate_of_change` | Temporal NDVI trajectory |
| `NDVI_minimum` | Minimum NDVI across composites |

---

## Repo structure

```
xcropstress/
├── data_generation.py        # Parametric synthetic dataset generation
├── train_model.py            # Random Forest training + evaluation
├── shap_analysis.py          # SHAP TreeExplainer + plot generation
├── XCropStress_Notebook.ipynb  # Full end-to-end notebook (Google Colab)
├── figures/                  # Output plots (confusion matrix, SHAP beeswarm, heatmap)
├── requirements.txt
└── README.md
```

> **Note:** Update these filenames to match your actual files before publishing.

---

## Quickstart

```bash
git clone https://github.com/YOUR_USERNAME/xcropstress.git
cd xcropstress
pip install -r requirements.txt
python data_generation.py   # generates synthetic_dataset.csv
python train_model.py       # trains RF, prints classification report
python shap_analysis.py     # generates SHAP figures
```

Or open `XCropStress_Notebook.ipynb` directly in Google Colab.

---

## Requirements

```
scikit-learn
shap
numpy
pandas
matplotlib
seaborn
```

Install with:
```bash
pip install -r requirements.txt
```

---

## Dataset parameterization

Spectral distributions were sourced from:

- **[S1]** Sharma et al. (2025). *Leveraging Sentinel-2 Data and Machine Learning for Drought Detection in India.* MDPI Remote Sensing, 17(18), 3159.
- **[S2]** Authors (2025). *Evaluating NDVI, GNDVI, EVI, and SAVI for Accurate Crop Classification Using Harmonized Landsat-Sentinel-2 Data — Mahalaxmi Kheda Village, Maharashtra.* ResearchGate.
- **[S3]** Authors (2025). *Machine Learning with SHAP Analysis for Spectral Index Classification of Indian Agricultural Land.* Journal of the Indian Society of Remote Sensing.

No raw satellite imagery is used. All data is generated from published statistics — fully reproducible without ESA/Copernicus access.

---

## Citation

If you use this work, please cite:

```
@article{jagtap2025xcropstress,
  title={XCropStress: A Controlled Simulation Study for Explainable Multi-Class Crop Stress Detection Using SHAP Feature Attribution on Sentinel-2 Spectral Indices},
  author={Jagtap, Rajvardhan Ajitrao and Lavhate, Sarang Santosh},
  year={2025},
  institution={Rajarambapu Institute of Technology}
}
```

> Update this with the actual venue/DOI once the paper is published.

*Department of Computer Science & Engineering, Rajarambapu Institute of Technology, Rajaramnagar, India*
