# Sentinel-2 Satellite Image Processing & Land Cover Classification using ESA SNAP

## Overview
This repository documents an end-to-end satellite remote sensing project focused on processing **Sentinel-2A optical satellite imagery** (`20240728T090601` scene) using the open-source **ESA SNAP (Sentinel Application Platform)** software. The project encompasses radiometric/geometric preprocessing, spectral band combination analyses, vegetation/water index calculation, supervised and unsupervised Land Use / Land Cover (LULC) classification algorithms, and rigorous confusion matrix accuracy assessments.

---

## Technical Specifications
* **Software:** ESA SNAP 10 / Sentinel-2 Toolbox
* **Satellite Platform:** Sentinel-2A (MultiSpectral Instrument - MSI, Level-1C)
* **Spatial Reference Systems:** UTM / WGS-84 (EPSG:32635) transformed to Romanian Stereo 70 (EPSG:31700)[cite: 4]
* **Spatial Resolutions:** 10m, 20m, and 60m resampled across 13 spectral bands[cite: 4]

---

## Project Methodology & Workflow

### 1. Preprocessing & Geometric Transformation
* **Resampling & Subsetting:** Harmonized spatial resolution across all bands to 10m using nearest neighbor interpolation, followed by spatial ROI subsetting[cite: 4].
* **Coordinate Reprojection:** Reprojected satellite rasters from native UTM/WGS84 zone 35N to the national **Stereo 70** projection system via inverse mapping algorithms[cite: 4].

### 2. Spectral Band Combinations & Index Math
* **False-Color Visualization:** Generated Natural Color (B4-B3-B2), False-Color Infrared (B8-B4-B3), and Shortwave Infrared (B12-B8-B3) RGB composite views for land feature discrimination[cite: 4].
* **NDVI Computation:** Calculated the Normalized Difference Vegetation Index using Band Math[cite: 4]:
  $$\text{NDVI} = \frac{\text{B8 (NIR)} - \text{B4 (Red)}}{\text{B8 (NIR)} + \text{B4 (Red)}}$$
  Applied custom threshold masks to categorize water ($<-0.1$), bare soil ($-0.1 \text{ to } 0.1$), grasslands ($0.1 \text{ to } 0.3$), and dense vegetation ($>0.5$)[cite: 4].
* **NDWI Computation:** Derived the Normalized Difference Water Index using shortwave and near-infrared channels (B12 & B8) via SNAP's Thematic Water Processing engine[cite: 4].

### 3. Image Classification Workflows
* **Unsupervised Classification (K-Means Clustering):**
  * *Scenario I:* 5 clusters using all 12 spectral bands (excluding B9)[cite: 4].
  * *Scenario II:* 5 clusters incorporating all bands plus derived NDVI and NDWI rasters[cite: 4].
  * *Scenario III:* High-resolution 20-cluster iteration using all spectral bands and environmental indices[cite: 4].
* **Supervised Classification (Maximum Likelihood Classifier):**
  * Digitized custom training vector containers across 5 land cover classes: Water, Forest, Vegetated Soil, Bare Soil, and Built-up Areas[cite: 4].
  * Extracted spectral signatures and executed Maximum Likelihood classification across 5,000 training samples[cite: 4].

### 4. Statistical Analysis & Accuracy Assessment
* **Scatter Plots & Histograms:** Analyzed class separability and spectral overlap (notably between built-up areas, bare soil, and shallow water bodies)[cite: 4].
* **Validation Pins:** Generated 50 stratified ground truth pins (10 per class) to evaluate classification precision[cite: 4].
* **Confusion Matrix Evaluation:** 
  * The **Maximum Likelihood Supervised Classifier** achieved an Overall Accuracy of **94%** and a Kappa Coefficient ($K$) of **92.5%**[cite: 4].
  * Unsupervised K-Means scenarios achieved 58% (Scenario 1) and 66% (Scenario 3) overall accuracy, highlighting the effectiveness of supervised training[cite: 4].

---

## Deliverables
* Processed & Reprojected Sentinel-2 Rasters (`.dim` / `.data`)[cite: 4]
* NDVI & NDWI Mask Products[cite: 4]
* Supervised & Unsupervised LULC Classification Maps[cite: 4]
* Statistical Scatter Plots, Class Histograms, and Confusion Matrices (`.xml` / `.txt`)[cite: 4]
<img width="598" height="365" alt="image_2026-09-14_204734811" src="https://github.com/user-attachments/assets/1e49a40c-5155-4f5c-8605-9678722dfc02" />
<img width="613" height="333" alt="image_2026-09-14_204643289" src="https://github.com/user-attachments/assets/fed06ba9-feb4-4328-a2d9-a4de78acc3b5" />
<img width="596" height="415" alt="image_2026-09-14_204454267" src="https://github.com/user-attachments/assets/a31ad789-4c49-4086-ba3e-9aa5cbf16848" />

---

## Author & Academic Context
* **Author:** Cofariu Diana-Elena[cite: 4]
* **Academic Context:** Coursework Project supervised by Prof. Habil. Dr. Ing. Valeria Ersilia Oniga, Faculty of Hydrotechnics, Geodesy and Environmental Engineering, Technical University "Gheorghe Asachi" of Iași (2026)[cite: 4].
