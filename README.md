# Photometric Classification of Galaxies, Quasars, and Stars using Machine Learning

This repository presents an implementation of the methodology described in  
**“Machine learning-based photometric classification of galaxies, quasars, emission-line galaxies, and stars”**  
(Zeraatgari et al., 2023).

The project focuses on the **three-class classification problem** (Galaxy, QSO, Star) and demonstrates the performance improvement obtained by combining **optical (SDSS DR17)** and **infrared (ALLWISE)** photometric information.

---

## Project Overview

Modern sky surveys generate vast photometric datasets, making spectroscopic classification expensive and impractical at scale. This project explores the use of supervised machine-learning models to classify astronomical objects using **multiband photometry alone**.

Two feature sets are evaluated:

- **Sample I (Optical):** SDSS DR17 photometric colors  
- **Sample II (Optical + Infrared):** SDSS DR17 + ALLWISE photometric colors  

The impact of infrared information on classification performance is analyzed across multiple machine-learning models.

---

## Dataset

- **Optical:** Sloan Digital Sky Survey (SDSS) Data Release 17  
- **Infrared:** ALLWISE Source Catalog  

**Classes:**
- Galaxy  
- Quasar (QSO)  
- Star  

**Final dataset (unbalanced):**

| Class   | Count |
|--------|-------|
| Galaxy | 52,621 |
| QSO    | 13,820 |
| Star   | 12,978 |

---

## Data Preprocessing

Key preprocessing steps include:

- Handling missing values and basic data inspection  
- Removal of non-informative identifiers (RA, DEC, object IDs, etc.)  
- Conversion of ALLWISE Vega magnitudes to **AB magnitudes**  
- Construction of **color indices**:
  - Optical: `u−g`, `g−r`, `r−i`, `i−z`
  - Optical + IR: `z−W1`, `W1−W2`
- Feature correlation analysis using heatmaps  

---

## Machine Learning Models

The following supervised models were implemented and evaluated:

- Random Forest (RF)  
- XGBoost (XGB)  
- k-Nearest Neighbors (KNN)  
- Artificial Neural Network (ANN) (MLP-based)  
- Soft Voting Classifier  
  *(RF and XGB weighted higher than KNN, following the reference paper)*

---

## Experimental Setup

The implementation follows a **two-part strategy inspired by the paper**:

### Part 1
- Random Forest trained on both feature sets  
- Used to establish baseline performance and feature importance  

### Part 2
- Multiple classifiers trained on the **unbalanced dataset**  
- Performance compared across models and feature sets  

**Evaluation metrics:**
- Precision  
- Recall  
- F1-score  
- Per-class and overall comparison  

---

## Results Summary

- All models show **improved performance** when infrared features are included  
- Optical + IR features consistently outperform optical-only features  
- RF and XGB achieve the strongest overall performance  
- Feature importance analysis highlights:
  - `W1−W2` and `z−W1` as the most informative features  

---

## Visualizations

The repository includes:

- Feature correlation heatmaps  
- Color–color scatter plots (Optical vs Optical + IR)  
- Feature importance plots from Random Forest  
- Model performance comparison tables  

These visualizations provide physical insight into why infrared data improves class separation.

---

## Scope and Limitations

- This implementation focuses on the **three-class classification problem**  
- Subclassification of galaxies (NG, ELG, AGN, etc.) and spectroscopic features are not included  
- Results are intended as a **reproducible validation** of the core claims of the reference paper  

---

## Reference

Zeraatgari et al.,  
*Machine learning-based photometric classification of galaxies, quasars, emission-line galaxies, and stars*,  
Monthly Notices of the Royal Astronomical Society (2023).  
arXiv:2311.02951
