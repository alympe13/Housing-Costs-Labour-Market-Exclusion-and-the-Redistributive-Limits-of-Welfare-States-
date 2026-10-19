# Replication Package for: "Housing Costs, Labour Market Exclusion and the Redistributive Limits of Welfare States: Evidence from a 21–Year European Macro Panel"

## 1. Overview
This replication package contains the full suite of R scripts used for data construction, validation, econometric modeling, and robustness checks for the manuscript submitted to the *International Journal of Social Economics*. 

The package is designed to provide 100% methodological transparency, allowing reviewers and readers to perfectly trace the steps from raw microdata aggregation to the final empirical tables presented in the paper.

## 2. Data Availability & Confidentiality
Please note that the core dataset relies on the **European Union Statistics on Income and Living Conditions (EU-SILC)** microdata. Due to strict data protection regulations and non-disclosure agreements enforced by Eurostat, the **raw microdata files (D, H, R, P files) cannot be shared publicly**. 

However, to facilitate full reproducible research, we provide the custom, bottom-up data-aggregation R script used to generate the macroeconomic variables, alongside the final aggregated macro-panel dataset (`Thesis_Final_Panel_Dataset_Bulletproof.csv`). This allows researchers to independently run all econometric models and validation checks without needing access to the restricted microdata.

## 3. Software Requirements
The code was written and tested in **R**. To execute the scripts seamlessly, please ensure the following R packages are installed:
* Data Manipulation: `dplyr`, `tidyr`, `stringr`, `data.table`
* API & Validation: `eurostat`
* Econometrics: `plm`, `lmtest`, `sandwich`, `car`
* Output & Formatting: `stargazer`

## 4. File Manifest
The repository/folder contains the following scripts, structured in logical order of execution:

### A. Data Construction & Validation
* **`Data_Aggregation_Pipeline.R`**: The master script that processes the raw EU-SILC microdata. It applies necessary patches (e.g., Malta SDC age categorisations), standardises variables, and applies cross-sectional weights to construct the national macro-aggregates.
* **`Eurostat_Validation_Script.R`**: An automated validation script that queries the official Eurostat API to download official macro-aggregates and calculates the Mean Absolute Error (MAE) against our constructed dataset.

### B. Econometric Analysis
* **`Econometric_Models_Script.R`**: Contains the baseline one-way fixed effects models with 1-year lagged independent variables. It applies Arellano clustered standard errors (robust to heteroskedasticity and serial correlation) using the `lmtest` and `sandwich` packages.

### C. Diagnostics & Robustness Checks (Requested during Peer Review)
* **`Robustness_Time_Effects_Script.R`**: Estimates the two-ways fixed effects models (incorporating country and year dummies) to control for EU-wide macroeconomic shocks, automatically exporting Table A3.
* **`Diagnostics_Hausman_VIF.R`**: Executes the Hausman specification test (justifying the fixed-effects approach over random-effects) and calculates the Variance Inflation Factor (VIF) to rule out multicollinearity.
* **`Robustness_Failed_System_GMM.R`**: Provided for absolute transparency. This script contains the initially attempted two-step System GMM dynamic panel model, which was ultimately abandoned (as noted in the manuscript's Limitations) due to severe instrument proliferation.

### D. Summary Statistics & Appendix Tables
* **`Correlation_Matrix_Script.R`**: Generates and exports the Pearson Correlation Matrix (Table A1).
* **`Data_Coverage_Script.R`**: Generates and exports the unbalanced panel coverage map per country (Table A2).

## 5. Instructions for Use
1. Save all `.R` scripts and the `Thesis_Final_Panel_Dataset_Bulletproof.csv` file in the same local directory.
2. Set that directory as your Working Directory in R (`setwd("path/to/folder")`) or open the folder as an RStudio Project.
3. You can execute any script from sections B, C, and D directly, as they all call the provided `.csv` dataset. 
4. The tables (A1, A2, A3) will be automatically exported to your working directory as `.doc` files.

## 6. Contact
For any questions regarding the code or the dataset, please contact the corresponding author.
