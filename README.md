# precipitation-downscaling-gee
GPM IMERG precipitation downscaling from 10 km to 1 km over Dhaka District using a deep learning MLP model trained on MODIS predictors via Google Earth Engine (2002–2024).
#  Precipitation Downscaling Using Deep Learning (GEE + xarray + Keras)

##  Live Project Page
 **[View Full Analysis](https://nabedist29.github.io/precipitation-downscaling-gee/)**

---

## Overview

This project statistically downscales NASA GPM IMERG monthly precipitation
from ~10 km to ~1 km resolution over Dhaka District, Bangladesh (2002–2024)
using a fully connected deep learning model (Multi-Layer Perceptron) trained
on multi-source MODIS satellite predictors extracted via Google Earth Engine.

---

## Key Features

- **Study Area:** Dhaka District, Bangladesh
- **Time Period:** January 2002 – December 2024
- **Resolution Enhancement:** ~10 km → ~1 km (82× spatial detail increase)
- **Training Data:** 276 monthly images × 25 coarse pixels (5×5 grid)
- **Inference Grid:** 2,050 pixels per time step (41×50 at 0.01°)

---

## Data Sources

| Variable | Dataset | Resolution |
|----------|---------|------------|
| Precipitation (target) | NASA GPM IMERG Monthly V07 | ~10 km |
| NDVI, EVI | MODIS MOD13Q1 | 250 m |
| LST Day & Night | MODIS MOD11A2 | 1 km |
| Evapotranspiration | MODIS MOD16A2GF | 500 m |
| Land Cover | MODIS MCD12Q1 | 500 m |
| Elevation (DEM) | USGS GTOPO30 | ~1 km |

---

## Methodology

1. Extract monthly multi-variable ImageCollection from GEE using `xee`
2. Load at 0.1° resolution (10 km) as training domain
3. Standardize predictors and target with `StandardScaler`
4. Train a 4-layer MLP (64→32→16→1) with Adam optimizer, MSE loss, 50 epochs
5. Load same collection at 0.01° resolution (1 km) as inference domain
6. Apply trained model → inverse-transform to mm/hr
7. Post-process: clip negatives + monthly 99th-percentile capping

---

## Model Performance

| Metric | Training | Validation | Test |
|--------|----------|------------|------|
| MSE (standardized) | 0.197 | 0.246 | ~0.25 |
| MAE (standardized) | 0.305 | 0.328 | ~0.33 |
| Loss reduction | ~50% over 50 epochs | | |

---

## Tools & Libraries

`Google Earth Engine` · `xee` · `xarray` · `TensorFlow/Keras` · `scikit-learn` · `pandas` · `numpy` · `geemap` · `Google Colab`

---

## Tutorial Credit

This project is adapted from:

> **Google Earth Engine Tutorial-176: Precipitation Downscaling using Deep Learning Modelling**
> by **Amir Hossein Ahrari** 

Adapted to Dhaka District, Bangladesh with extended post-processing and methodological annotation.

---

## Author

**Istiaque Ahamed Nabed**
Department of Disaster Science and Climate Resilience, University of Dhaka
🔗 [GitHub Portfolio](https://github.com/nabedist29)
