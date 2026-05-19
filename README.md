# 🌲 Forest Cover Type Prediction via XGBoost

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-v2.0-FF6F20?style=flat-square&logo=xgboost&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)

An end-to-end Machine Learning classification framework designed to predict dominant forest cover types across heavily imbalanced environments. Utilizing **581,012 spatial samples** from the **US Forest Service (USFS)**, this project eliminates the need for expensive physical site surveys by mapping geographical, topographic, and geological data directly into ecological forest categories.

---

## 🎯 Project Overview & Objectives

Traditional ecological surveys are slow and resource-intensive. This project leverages advanced gradient boosting to automate land-use mapping.

* **Massive Scale:** Processes **581,012 records** with 54 structural features.
* **Imbalance Handling:** Accurately models rare ecological niches without destructive synthetic oversampling.
* **Production Ready:** Evaluated over a rigorous validation split of **116,203 test samples**.

---

## 🧭 Dataset Architecture

The model ingests 54 cartographic variables (all numerical/encoded, requiring no subjective manual labeling):

* **Topographic Profile:** Elevation (meters), Aspect (degrees), Slope (degrees).
* **Spatial Distances:** Horizontal/Vertical distance to Hydrology, Roadways, and Fire Points.
* **Hillshade Coefficients:** Solar illumination indices captured at 9 AM, Noon, and 3 PM (summer solstice).
* **Wilderness Areas:** 4 binary indicators mapping localized wilderness zones (*Rawah, Neota, Comanche Peak, Cache la Poudre*).
* **Micro-Geological Soil Types:** 40 binary variables mapping complex USFS soil classifications.

---

## 🚀 Model Performance & Key Results

The core **XGBoost** classifier achieved a powerful **83.08% Global Accuracy** score. 

### Granular Metrics Report

| Class Name (Cover_Type) | Precision | Recall | F1-Score | Support |
| :--- | :---: | :---: | :---: | :---: |
| **1: Spruce/Fir** | 0.82 | 0.80 | 0.81 | 42,368 |
| **2: Lodgepole Pine** | 0.83 | 0.87 | 0.85 | 56,661 |
| **3: Ponderosa Pine** | 0.84 | 0.88 | 0.86 | 7,151 |
| **4: Cottonwood/Willow** | 0.85 | 0.82 | 0.83 | 549 |
| **5: Aspen** | 0.86 | **0.43** | 0.57 | 1,899 |
| **6: Douglas-fir** | 0.80 | 0.68 | 0.74 | 3,473 |
| **7: Krummholz** | **0.92** | 0.86 | 0.89 | 4,102 |

### 🧠 Strategic Insights from the Confusion Matrix

1.  **Dominant Class Stability:** The model shows high robustness within the most populated classes (Spruce/Fir and Lodgepole Pine), establishing strong baseline stability.
2.  **High-Altitude Precision:** **Krummholz (Class 7)** achieved a stellar **0.92 Precision**, meaning the model perfectly learned the strict high-elevation boundaries where this species grows, eliminating false alarms.
3.  **The Overlap Challenge:** **Aspen (Class 5)** yielded a low Recall of **0.43**. The matrix revealed that 1,028 actual Aspen locations were misclassified as Lodgepole Pine due to intense territorial and altitudinal competition in nature.

---

## 📊 Feature Importance: What the Model Learned

The model successfully bypassed abstract assumptions and mapped real-world biophysical constraints. The **Top 5 features** driving the tree layout distribution are:

🥇 Feature 13 (Wilderness_Area_4 / Cache la Poudre) -> 0.0964

🥈 Feature 00 (Elevation)                          -> 0.0773

🥉 Feature 52 (Soil_Type_39: Leighcan-Moran)        -> 0.0553

🏅 Feature 51 (Soil_Type_38: Leighcan-Catamount)    -> 0.0548

🏅 Feature 53 (Soil_Type_40: Moran-Cryaquolls)      -> 0.0550
