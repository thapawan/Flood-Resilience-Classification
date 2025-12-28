# Flood Resilience Classification Framework

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.12345678.svg)](https://doi.org/10.5281/zenodo.12345678) <!-- Optional: Add when you have a DOI -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Earth Engine](https://img.shields.io/badge/Google%20Earth%20Engine-Enabled-brightgreen)](https://skilful-boulder-440618-e7.projects.earthengine.app/view/flood-resilience)

A data-driven, reproducible framework for classifying landscape flood resilience into distinct, statistically validated categories using annual satellite embeddings in Google Earth Engine.

> **Key Publication:** This code and methodology support the findings presented in:  
> *"A Data-Driven Framework for Post-Flood Recovery and Resilience Classification Using Multi-Temporal Satellite Embeddings"* (Manuscript in Prep./Submitted).

---

## 🚀 Overview

This repository provides a complete implementation of a novel framework that quantifies post-flood ecosystem resilience. Moving beyond arbitrary thresholds, it uses **data-driven percentile cuts** on trajectories derived from **multi-temporal satellite embeddings** (Google's `GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`) to objectively classify pixels into four resilience classes:
- **Unaffected**
- **Fully Resilient**
- **Recovering**
- **Non-Resilient**

The method is validated through stratified sampling and statistical hypothesis testing, demonstrating a strong relationship between resilience class and topographic drivers like elevation.

## ✨ Features

*   **Objective Classification:** Eliminates subjective resilience thresholds using data-driven percentiles (25th, 75th).
*   **Leverages Advanced Data:** Uses high-dimensional satellite embeddings for a holistic view of land surface change.
*   **Fully Scalable:** Built entirely in Google Earth Engine for planetary-scale analysis.
*   **Reproducible Workflow:** Clear, step-by-step Jupyter Notebooks and GEE scripts.
*   **Comprehensive Validation:** Includes scripts for stratified sampling and a 4-part statistical hypothesis test (ANOVA, correlation, logical ordering, environmental correlates).

## 📁 Repository Structure

```
Flood-Resilience-Classification-GEE/
│
├── 01_GEE_Resilience_Classification.js
│   └── Main Google Earth Engine script. Computes baseline, shock, recovery, permanence, and applies the data-driven classification logic.
│
├── 02_Data_Export_and_Sampling.js
│   └── GEE script to export results (GeoTIFFs) and perform stratified random sampling for validation.
│
├── 03_Statistical_Validation_Analysis.ipynb
│   └── Python Jupyter Notebook for hypothesis testing (ANOVA, correlations, box plots) using exported sample data.
│
├── config/
│   └── study_area.geojson          # GeoJSON boundary for the Hamburg, Iowa study area.
│
├── data/
│   ├── sample_points.csv           # Example stratified validation sample data.
│   └── class_metrics_summary.csv   # Example summary statistics for each resilience class.
│
├── docs/
│   └── Methodology_Workflow.png    # Visual overview of the 6-step framework.
│
├── environment.yml                 # Conda environment for reproducing the Python analysis.
└── README.md                       # This file.
```

## 🛠️ Installation & Usage

### 1. Prerequisites
*   A **Google Earth Engine Account** (Sign up [here](https://earthengine.google.com/signup/)).
*   **Google Cloud Storage Bucket** (for exporting results).
*   For local analysis: **Python 3.9+** with Jupyter. Use the provided `environment.yml` to create a conda environment:
    ```bash
    conda env create -f environment.yml
    conda activate flood-resilience
    ```

### 2. Run the Framework in GEE

1.  **Open the GEE Code Editor.**
2.  **Load the Scripts:** Upload `01_GEE_Resilience_Classification.js` and `02_Data_Export_and_Sampling.js`.
3.  **Configure Parameters:** In the first script, adjust:
    *   `studyArea`: Import your own region of interest (ROI) or use the provided GeoJSON.
    *   `startYear`, `endYear`: Define your analysis period (e.g., `2017`, `2024`).
    *   `floodYear`: Set the year of the disturbance event (e.g., `2019`).
4.  **Run and Inspect:** Execute `01_GEE_Resilience_Classification.js`. The console will print class distributions, and the map will display the resilience classification.
5.  **Export Results:** Run `02_Data_Export_and_Sampling.js` to export the resilience map as a GeoTIFF to your Google Cloud Storage and generate validation sample points.

### 3. Perform Statistical Validation (Local)

1.  **Export Data:** Download the sample points CSV from GEE/Cloud Storage.
2.  **Open Jupyter Notebook:** Launch Jupyter and open `03_Statistical_Validation_Analysis.ipynb`.
3.  **Update File Paths:** Point the notebook to your downloaded `sample_points.csv`.
4.  **Run All Cells:** The notebook will generate:
    *   Summary statistics (mean Shock, Recovery, Permanence per class).
    *   ANOVA and Tukey HSD results for class distinctiveness.
    *   Correlation matrices for internal consistency.
    *   Box plots (e.g., elevation vs. class).

## 📊 Key Results from the Case Study (Hamburg, IA, 2019 Floods)

Applying this framework to a 100 km² area revealed:
*   **Class Distribution:** Unaffected (30.4%), Fully Resilient (24.8%), Recovering (37.7%), Non-Resilient (7.1%).
*   **Statistical Validation:** Resilience classes were statistically distinct (ANOVA, p < 0.001).
*   **Primary Driver:** Elevation was a highly significant predictor of resilience class (p < 0.001), with higher areas more resilient.
*   **Novel Finding:** Identification of a "Negative Recovery" class (Non-Resilient), showing continued post-flood degradation.

## 🤝 How to Cite

If you use this framework or code in your research, please cite the associated manuscript (details TBD upon publication). For now, you can cite this repository:

> Author. (2024). Flood-Resilience-Classification-GEE: A Data-Driven Framework for Post-Flood Resilience Classification using Satellite Embeddings. GitHub repository. https://github.com/thapawan/Flood-Resilience-Classification-GEE

**BibTeX:**
```bibtex
@software{Flood_Resilience_GEE_2024,
  author = {Author},
  title = {Flood-Resilience-Classification-GEE},
  year = {2024},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/thapawan/Flood-Resilience-Classification-GEE}}
}
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

*   This research was supported by [Your Institution/Funding Body].
*   Built using [Google Earth Engine](https://earthengine.google.com/).
*   Leverages the annual satellite embedding dataset (`GOOGLE/SATELLITE_EMBEDDING/V1/ANNUAL`).

## 📧 Contact

For questions, collaborations, or issues, please open a [GitHub Issue](https://github.com/thapawan/Flood-Resilience-Classification-GEE/issues) or contact pthapa2@crimson.ua.edu.
```
