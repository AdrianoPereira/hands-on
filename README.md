# Forecast Evaluation Hands-on

This repository provides a **hands-on notebook series** for evaluating deep learning architectures for **precipitation nowcasting over Latin America**. The workflow demonstrates end-to-end steps — from loading model outputs to generating categorical verification metrics and visual diagnostic plots.

**Authors:**
- Adriano P. Almeida (adriano.almeida@inpe.br)
- Alan J. P. Calheiros (alan.calheiros@inpe.br)

---

## 📘 Overview

The hands-on material focuses on **evaluating the performance of precipitation forecasts** derived from several deep learning models, using data stored in NetCDF format and versioned with **Git Large File Storage (Git LFS)**.
It covers:

* Loading and managing multi-dimensional forecast data with `xarray`;
* Computing key verification metrics (POD, FAR, CSI, Bias);
* Visualizing forecasts vs. ground truth fields using `cartopy` and `matplotlib`;
* Building multi-panel **performance diagrams** for comparative analysis.

---

## 🧠 Architectures Evaluated

Each model represents a different paradigm in spatio-temporal modeling:

* **Persistence** (baseline)
* **RIKEN DL Nowcast**
* **AFNO** — Adaptive Fourier Neural Operator
* **InceptionV4**
* **ResNet**
* **Xception**

All models are evaluated under the same experimental protocol for fair comparison.

---

## 📂 Repository Structure

```
.
├── notebooks/
│   ├── Evaluation_Forecasts.ipynb     # Main evaluation and visualization workflow
│
├── data/
│   └── dl-nowcasting-precipitation-latam/
│       ├── <Architecture>/
│       │   ├── FSCT1/
│       │   ├── FSCT2/
│       │   └── ...
│       └── ...
│
├── .gitattributes                     # Tracks large data files with Git LFS
├── README.md
└── requirements.txt
```

---

## 📦 Data Availability via Git LFS

All NetCDF data files used in this repository are stored and versioned using **Git Large File Storage (LFS)**.
To ensure the datasets are properly downloaded, please install Git LFS before cloning:

```bash
# Install Git LFS (Linux example)
sudo apt install git-lfs

# Initialize Git LFS
git lfs install

# Clone the repository (LFS files will be fetched automatically)
git clone https://github.com/<user>/<repo>.git
cd <repo>

# If necessary, manually pull large files
git lfs pull
```

The `.gitattributes` file in the root directory automatically tracks large files (e.g., `.nc`, `.tif`, `.h5`, `.dat.gz`) under Git LFS to prevent repository bloat.

---

## ⚙️ Dependencies

Install all required packages using:

```bash
pip install -r requirements.txt
```

Minimum environment:

* Python ≥ 3.10
* xarray, numpy, pandas, matplotlib, cartopy
* netCDF4 (for reading `.nc` files)

---

## 🌎 Dataset Domain

* **Region:** Latin America
* **Latitude:** -55° to 33°
* **Longitude:** -120° to -24°
* **Resolution:** 0.1° × 0.1°
* **Temporal Resolution:** 1 hour
* **Forecast Horizons:** 1–6 hours
* **Thresholds:** 0.1, 1.0, 5.0, 10.0 mm/h

Each dataset includes:

* `precip_obs` — observed precipitation (ground truth)
* `precip_fct` — model forecast precipitation

---

## 📊 Evaluation Metrics

The categorical evaluation is based on four contingency outcomes:

| Term | Description                                    |
| ---- | ---------------------------------------------- |
| TP   | True Positive (forecast and observed event)    |
| FP   | False Positive (forecasted event not observed) |
| FN   | False Negative (missed observed event)         |
| TN   | True Negative (no event in both)               |

### Derived Metrics

| Metric   | Formula               | Interpretation                  |
| -------- | --------------------- | ------------------------------- |
| **POD**  | TP / (TP + FN)        | Detection capability            |
| **FAR**  | FP / (TP + FP)        | Overforecasting ratio           |
| **CSI**  | TP / (TP + FP + FN)   | Overall forecast skill          |
| **Bias** | (TP + FP) / (TP + FN) | Over/under-forecasting tendency |

---

## 📈 Visualization Modules

* **Forecast Maps:** compare model output with observed precipitation.
* **CSI vs Horizon plots:** evaluate forecast degradation across lead times.
* **Performance Diagrams:** combine POD, FAR, CSI, and Bias in a single visual summary.

Each diagram includes:

* **CSI contours** (dashed gray lines)
* **Bias lines** (dotted)
* **Architectures** represented by colors
* **Horizons** represented by marker shapes

---

## 🧩 Hands-on Objective

By the end of this notebook series, participants will:

1. Understand how to compute and interpret key forecast verification metrics.
2. Visualize model performance across thresholds and horizons.
3. Compare multiple deep learning architectures under consistent conditions.
4. Build reproducible evaluation pipelines for nowcasting systems.

---

## 📚 References

* Wilks, D. S. (2011). *Statistical Methods in the Atmospheric Sciences*. Academic Press.
* Hogan, R. J., & Mason, I. B. (2012). Deterministic forecasts of binary events. *Meteorological Applications*, 19(1), 45–59.
* Schaefer, J. T. (1990). The Critical Success Index as an indicator of forecast skill. *Weather and Forecasting*, 5(4), 570–575.
* Schultz, D. M., & Tewari, M. (2021). Can machine learning improve weather forecasts? *Bulletin of the American Meteorological Society*, 102(4), E716–E729.
* Kubota, T. et al. (2020). Global Satellite Mapping of Precipitation (GSMaP): Algorithm updates and products. *IEEE Transactions on Geoscience and Remote Sensing*, 58(7), 3911–3924.

---

## 🤝 Acknowledgements

This repository is part of the **AINPP (AI for Nowcasting Pilot Project)**, dedicated to building standardized evaluation pipelines for AI-based precipitation forecasting over Latin America.
All datasets are distributed via **Git LFS** for reproducibility and version control.
