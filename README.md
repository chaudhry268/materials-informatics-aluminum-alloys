# Application of Materials Informatics to Predict Microstructure–Mechanical Property Correlation in Non-Heat-Treatable Aluminum Alloys

A materials informatics framework combining machine learning regression with Markov Chain Monte Carlo (MCMC) sampling to predict and extract relationships between elemental composition, temper designation, and mechanical properties of 5xxx series (non-heat-treatable) aluminum alloys.

**Bachelor's Thesis** — Institute of Metallurgy and Materials Engineering, Faculty of Chemical and Materials Engineering, University of the Punjab, Lahore  
Session 2019–2023

## Motivation

Non-heat-treatable aluminum alloys (5xxx series) derive their strength from solid-solution strengthening and strain hardening rather than precipitation hardening. Designing these alloys for specific applications is complex and time-consuming because of the intricate composition–property relationships involved. Traditional trial-and-error experimentation is inefficient and costly.

This project applies a materials informatics approach to:
- Analyze the relationships between alloy composition, temper designation, and mechanical properties
- Accelerate alloy development through data-driven property prediction
- Extract authentic structure–property relationships using MCMC sampling on top of ML predictive models

## Problem Statement

*"Applying Materials Informatics to Enhance Aluminum Alloy Understanding and Performance"*

Optimizing 5xxx series aluminum alloys for specific applications is challenging due to intricate composition–property relationships and the non-heat-treatable nature of the series. This work unravels correlations between alloy composition, processing (temper designation), and performance using a combined ML + MCMC methodology.

## Dataset

- **Alloy system:** 5xxx series aluminum alloys (non-heat-treatable)
- **Alloys included:** A5005, A5042, A5050, A5052, A5056, A5082, A5086, A5154, A5182, A5251, A5254, A5454, A5652, A5754, A5N01
- **Input features (13):** Temper designation (X, n) and composition in wt% (Al, Mg, Mn, Fe, Si, Cu, Cr, Ti, Zn)
- **Target properties (3):** 0.2% Proof Stress (MPa), Ultimate Tensile Strength (MPa), Elongation (%)

## Methodology

The workflow consists of data extraction → ML model training & validation → property prediction → MCMC sampling for relationship extraction.

### Machine Learning Models

| Model | Purpose |
|---|---|
| Linear Regression | Baseline linear predictor |
| Random Forest Regression | Ensemble of decision trees, captures non-linearity |
| Elastic Net Regression | Hybrid L1 + L2 regularization for feature selection |

### Validation

- **Leave-One-Out Cross-Validation (LOOCV)** — extreme case of K-fold CV, each record used once for testing while others are used for training
- **Root Mean Square Error (RMSE)** — used as the accuracy metric

### Markov Chain Monte Carlo Sampling

MCMC sampling is applied on top of the trained ML model to extract authentic relationships between explanatory variables (composition, temper designation) and target mechanical properties — going beyond what standard correlation analysis reveals.

## Key Results

### Model Accuracy (RMSE, lower is better)

| Property | Linear Regression | Random Forest | Elastic Net |
|---|---|---|---|
| 0.2% Proof Stress (MPa) | **16.85** | 19.59 | 23.35 |
| Tensile Strength (MPa) | 14.85 | **13.52** | 18.94 |
| Elongation (%) | 1.73 | **1.33** | 1.69 |

**Random Forest achieved the best overall accuracy**, particularly for tensile strength and elongation, owing to its robustness against outliers and its ability to capture non-linear composition–property relationships.

### Pearson Correlations with Mechanical Properties

| Element / Designation | Proof Stress (r) | Tensile Strength (r) | Elongation (r) |
|---|---|---|---|
| n (temper extent) | **+0.71** | +0.51 | **−0.61** |
| Mg | **+0.66** | **+0.85** | +0.28 |
| Al | −0.64 | −0.84 | −0.29 |
| Cu | −0.34 | −0.59 | −0.21 |
| Cr | +0.24 | +0.47 | +0.11 |
| Mn | +0.13 | +0.18 | +0.23 |

### Key Findings

1. **n (temper designation)** is directly related to tensile strength and proof stress, and inversely related to elongation.
2. **Higher proof stress** is associated with higher X, higher Fe/Mn, and lower Si/Ti/Cu/Cr/Zn content.
3. **Tensile strength** is dominantly affected by Mn, Al, Mg, Cu, and n.
4. **Improved overall mechanical performance** is achieved by increasing Mg/Mn content and decreasing Al content.
5. A general trade-off is observed: as tensile strength increases, elongation decreases — a well-known pattern in metals, confirmed here through data.
6. Property prediction accuracy is strongly dependent on the quality and quantity of training data.

## Repository Structure

- **data/** — Compiled 5xxx series alloy dataset
- **notebooks/** — Jupyter notebooks for data exploration, model training, model comparison, and MCMC sampling
- **src/** — Python source files for preprocessing, models, validation, and MCMC
- **results/figures/** — Correlation plots, RMSE comparison plots, and MCMC histograms
- **requirements.txt** — Python dependencies
- **README.md** — This file

## Reproduce

Clone the repository and install dependencies:

- `git clone https://github.com/chaudhry268/materials-informatics-aluminum-alloys.git`
- `cd materials-informatics-aluminum-alloys`
- `pip install -r requirements.txt`
- `jupyter notebook notebooks/02_model_training.ipynb`

Or open directly in Colab:  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chaudhry268/materials-informatics-aluminum-alloys/blob/main/notebooks/02_model_training.ipynb)

## Tech Stack

`Python` · `pandas` · `NumPy` · `scikit-learn` · `matplotlib` · `seaborn` · `PyMC / emcee` (for MCMC)

## Conclusion and Outlook

This work proposes a materials informatics approach that combines ML predictive modeling with MCMC sampling to extract authentic relationships between alloy composition, temper designation, and mechanical properties of 5xxx series aluminum alloys. Unlike conventional regression approaches that have limitations in attributing contributions of individual explanatory variables, the proposed method determines how each feature influences the predicted property through MCMC-derived distributions.

**Design recommendation from this work:** To simultaneously improve proof stress, tensile strength, and elongation in 5xxx Al alloys, **increase Mg and Mn content and decrease Al content.**

The extracted relations are specific to the compiled dataset; enlarging the dataset will likely refine the relationships. Sufficient, reliable data is therefore essential for training ML models with adequate predictive accuracy — low accuracy directly compromises the reliability of MCMC-drawn distributions.

## Future Work

- Expand the dataset with experimental EBSD and micrograph-based microstructural features (grain size, texture index, second-phase particle fraction)
- Apply CNN-based models to microstructural images for direct image-to-property prediction
- Extend the framework to heat-treatable alloys (6xxx, 7xxx) for comparative study
- Integrate with high-throughput DFT data for fundamental alloying descriptors
- Build an active learning loop for targeted experimental validation

## Author

**Muhammad Waseem Chaudhry**  
B.Sc. Metallurgy and Materials Engineering (2019–2023)  
Institute of Metallurgy and Materials Engineering, University of the Punjab, Lahore  

Research interests: Materials informatics · Machine learning for alloy design · Microstructure–property relationships · Non-heat-treatable aluminum alloys  

📧 [waseem19mmes2320@gmail.com]  
🔗 [https://www.linkedin.com/in/waseem-chaudhry-552477247/]

## Project Team

This work was completed as a group bachelor's thesis with:
- Muhammad Fakhir (19MME-S1-333)
- Taha Khalid (19MME-S2-305)
- Muhammad Waseem Chaudhry (19MME-S2-320)

## Supervisor

**Dr.-Ing. Waseem Amin**  
Institute of Metallurgy and Materials Engineering, University of the Punjab, Lahore

## License

MIT License — see [LICENSE](LICENSE) file.

## Acknowledgments

We gratefully acknowledge our supervisor Dr.-Ing. Waseem Amin for his guidance, and the faculty of the Institute of Metallurgy and Materials Engineering at the University of the Punjab for their support. Special thanks to Mr. Faisal Hussain, Mr. Umar Farooq, Mr. Usama Rasheed, and Mr. Ahmad Mubarik for their contributions to this work.

## Citation

If you reference this work, please cite:

> Fakhir, M., Khalid, T., & Chaudhry, M. W. (2023). *Application of Materials Informatics to Predict Microstructure–Mechanical Property Correlation in Non-Heat-Treatable Aluminum Alloys* (Bachelor's thesis). Institute of Metallurgy and Materials Engineering, University of the Punjab, Lahore.
