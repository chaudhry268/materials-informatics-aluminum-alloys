# Application of Materials Informatics to Predict Microstructure–Mechanical Property Correlation in Non-Heat-Treatable Aluminum Alloys

A materials informatics framework combining machine learning regression with 
Markov Chain Monte Carlo (MCMC) sampling to predict and extract relationships 
between elemental composition, temper designation, and mechanical properties 
of 5xxx series (non-heat-treatable) aluminum alloys.

**Bachelor's Thesis** — Institute of Metallurgy and Materials Engineering,  
Faculty of Chemical and Materials Engineering, University of the Punjab, Lahore  
Session 2019–2023

## Motivation

Non-heat-treatable aluminum alloys (5xxx series) derive their strength from 
solid-solution strengthening and strain hardening rather than precipitation 
hardening. Designing these alloys for specific applications is complex and 
time-consuming because of the intricate composition–property relationships 
involved. Traditional trial-and-error experimentation is inefficient and costly.

This project applies a materials informatics approach to:
- Analyze the relationships between alloy composition, temper designation, 
  and mechanical properties
- Accelerate alloy development through data-driven property prediction
- Extract authentic structure–property relationships using MCMC sampling 
  on top of ML predictive models

## Problem Statement

*"Applying Materials Informatics to Enhance Aluminum Alloy Understanding and Performance"*

Optimizing 5xxx series aluminum alloys for specific applications is challenging 
due to intricate composition–property relationships and the non-heat-treatable 
nature of the series. This work unravels correlations between alloy composition, 
processing (temper designation), and performance using a combined ML + MCMC 
methodology.

## Dataset

- **Alloy system:** 5xxx series aluminum alloys (non-heat-treatable)
- **Alloys included:** A5005, A5042, A5050, A5052, A5056, A5082, A5086, A5154, 
  A5182, A5251, A5254, A5454, A5652, A5754, A5N01
- **Input features (13):** 
  - Temper designation: X, n
  - Composition (wt%): Al, Mg, Mn, Fe, Si, Cu, Cr, Ti, Zn
- **Target properties (3):**
  - 0.2% Proof Stress (MPa)
  - Ultimate Tensile Strength (MPa)
  - Elongation (%)

## Methodology

The workflow consists of data extraction → ML model training & validation → 
property prediction → MCMC sampling for relationship extraction.

### Machine Learning Models

| Model | Purpose |
|---|---|
| Linear Regression | Baseline linear predictor |
| Random Forest Regression | Ensemble of decision trees, captures non-linearity |
| Elastic Net Regression | Hybrid L1 + L2 regularization for feature selection |

### Validation

- **Leave-One-Out Cross-Validation (LOOCV)** — extreme case of K-fold CV, 
  each record used once for testing while others are used for training
- **Root Mean Square Error (RMSE)** — used as the accuracy metric

### Markov Chain Monte Carlo Sampling

MCMC sampling is applied on top of the trained ML model to extract authentic 
relationships between explanatory variables (composition, temper designation) 
and target mechanical properties — going beyond what standard correlation 
analysis reveals.

## Key Results

### Model Accuracy (RMSE, lower is better)

| Property | Linear Regression | Random Forest | Elastic Net |
|---|---|---|---|
| 0.2% Proof Stress (MPa) | **16.85** | 19.59 | 23.35 |
| Tensile Strength (MPa) | 14.85 | **13.52** | 18.94 |
| Elongation (%) | 1.73 | **1.33** | 1.69 |

**Random Forest achieved the best overall accuracy**, particularly for tensile 
strength and elongation, owing to its robustness against outliers and its 
ability to capture non-linear composition–property relationships.

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

1. **n (temper designation)** is directly related to tensile strength and proof 
   stress, and inversely related to elongation.
2. **Higher proof stress** is associated with higher X, higher Fe/Mn, and lower 
   Si/Ti/Cu/Cr/Zn content.
3. **Tensile strength** is dominantly affected by Mn, Al, Mg, Cu, and n.
4. **Improved overall mechanical performance** is achieved by increasing Mg/Mn 
   content and decreasing Al content.
5. A general trade-off is observed: as tensile strength increases, elongation 
   decreases — a well-known pattern in metals, confirmed here through data.
6. Property prediction accuracy is strongly dependent on the quality and 
   quantity of training data.

## Repository Structure
