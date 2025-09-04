# Soil Health Data Analysis and Modelling

This repository contains code for **processing, cleaning, imputing, modelling, and analysing soil data**. The project is based on the *SoilHealthDB* dataset, which compiles 5,907 comparisons across 42 soil health indicators and 46 background indicators from 321 scientific papers.

---

## Dataset

- **Source:** [SoilHealthDB (V2)] – available on [GitHub](https://github.com/jinshijian/SoilHealthDB), with details in the publication: Jian, J., Du, X. & Stewart, R.D. *A database for global soil health assessment.* Scientific Data 7, 16 (2020). https://doi.org/10.1038/s41597-020-0356-3
- **Contents:**  
  - 42 Soil health indicators (e.g., bulk density, cation exchange capacity, yield).  
  - 46 Background indicators (e.g., climate, elevation, soil texture).  
- **Format:** Provided as both `.xlsx` and `.csv`. The code primarily works with the `.xlsx` file to avoid data corruption (e.g., auto-conversion of IDs to dates).  
- **Access:** This repository does **not include the dataset**. Instead, the code will automatically download it from the official source.  

---

## Disclaimer

I developed this code during my research internship to investigate the application of machine learning methods to recent soil health datasets.  

- An **official repository** for this project will be maintained by lead investigators (Dr Stuart King & Prof Jonathan Hillier).  
- The **results of this code** will be used in future publications.  
- This repository is intended for **demonstration purposes** and may not represent the final version of the analysis pipeline.  

**Important Usage Terms:**  
- Allowed for individual, academic, research, and commercial use.  
- Cannot be repackaged or resold without written permission.  
- If you use this dataset, please cite both this GitHub page and the associated publications (see [License & Citation](#license--citation) below).

---

## Code Structure

### 1. Data Cleaning
The pipeline includes:
- Fixing misformatted Experiment IDs.  
- Removing redundant or inconsistent columns.  
- Handling unit inconsistencies using the provided "comments".  
- Missing data imputation for **sand, silt, and clay** percentages using USDA soil texture triangle.  
- Excluding outliers based on thresholds.

### 2. Data Visualization
The code provides multiple visualizations to explore and assess the dataset, including:  
- Plots of missing data patterns.  
- Checks for replicated Experiment IDs and site coordinates.  
- Scatterplot matrices with Pearson and Spearman correlation coefficients.  
- Histograms of soil health indicators.  
- Cumulative distribution plots for cash crop yield.

### 3. Modelling
A unified modelling function was developed supporting categorical predictors and different input structures.  
Implemented regression models include:
- Linear Regression  
- Ridge Regression  
- Support Vector Regression (SVR)  
- KNN Regression  
- Decision Tree  
- Random Forest  
- XGBoost (standard & Random Forest)  
- Generalized Additive Model (GAM)  

**Model Evaluation:**  
- MAE, RMSE, R²  
- K-fold cross-validation  
- Feature importance (permutation, SHAP, coefficients, partial dependence plots)  

### 4. Missing Data Imputation
Best-performing models were used to impute missing values for key soil indicators:

<table>
  <tr>
    <th>Feature</th>
    <th>Model Used</th>
    <th>Imputed Values</th>
  </tr>
  <tr>
    <td>CEC (Control)</td>
    <td>GAM</td>
    <td>351</td>
  </tr>
  <tr>
    <td>CEC (Treatment)</td>
    <td>SVR</td>
    <td>351</td>
  </tr>
  <tr>
    <td>BD (Control)</td>
    <td>XGBoost RF</td>
    <td>654</td>
  </tr>
  <tr>
    <td>BD (Treatment)</td>
    <td>Random Forest</td>
    <td>612</td>
  </tr>
</table>

### 5. Statistical Testing
Statistical analyses were conducted to evaluate the effects of different conservation treatments:
  - Shapiro-Wilk (normality check)  
  - Mann-Whitney U test  
  - Wilcoxon signed-rank test  

---

## License & Citation

This repository contains only code for cleaning, modelling, and analysing soil health data. The code is released under the MIT Licenses and may be used, modified, and distributed freely. 

The SoilHealthDB [dataset](#dataset) is not included in this repository. For details of the dataset, please see the SoilHealthDB GitHub page and the related publication. The dataset may be used for academic, research, and commercial purposes, but cannot be repackaged or resold without written permission. 

If you use or adapt this code in your own work, please include a reference to this repository (https://github.com/mayahua/Soil_Health) in addition to citing the original dataset. When available, please also cite our forthcoming publication based on this work.

---

## Contacts

- Code developed by: Maya Hua [📧](mailto:maya.hua@outlook.com) | MSc @ Univeristy of Edinburgh, BSc @ University of Bristol, looking for PhD opportunities in AI4Science or related industry roles.
- Supervisors: Dr Stuart King [📧](mailto:s.king@ed.ac.uk); Prof Jonathan Hillier [📧](mailto:jonathan.hillier@ed.ac.uk)
