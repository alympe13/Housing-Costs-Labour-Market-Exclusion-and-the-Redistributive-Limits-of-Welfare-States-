# Replication Package for: "Housing Costs, Labour Market Exclusion and the Redistributive Limits of Welfare States: Evidence from a 21–Year European Macro Panel"

## 1. Overview
This replication package contains the full suite of R scripts used for data construction, validation, econometric modeling, and robustness checks for the manuscript submitted to the *International Journal of Social Economics*. 

The package is designed to provide 100% methodological transparency, allowing reviewers and readers to perfectly trace the steps from raw microdata aggregation to the final empirical tables presented in the paper.

## 2. Data Availability & Confidentiality
Please note that the core dataset relies on the **European Union Statistics on Income and Living Conditions (EU-SILC)** microdata. Due to strict data protection regulations and non-disclosure agreements enforced by Eurostat, the **raw microdata files (D, H, R, P files) cannot be shared publicly**. 

However, to facilitate full reproducible research, we provide the custom, bottom-up data-aggregation R script used to generate the macroeconomic variables, alongside the final aggregated macro-panel dataset (`Thesis_Final_Panel_Dataset_Bulletproof.csv`). This allows researchers to independently run all econometric models and validation checks without needing access to the restricted microdata.

## 3. Software Requirements
The code was written and tested in **R**. To execute the scripts seamlessly, please ensure the following R packages are installed:
- Data Manipulation: `dplyr`, `tidyr`, `stringr`, `data.table`
- API & Validation: `eurostat`
- Econometrics: `plm`, `lmtest`, `sandwich`, `car`
- Output & Formatting: `stargazer`

## 4. File Manifest
The repository contains the following scripts, structured in logical order of execution:

### A. Data Construction & Validation
- **`EUSILC DATABASE ALL YEARS`**: The master script that processes the raw EU-SILC microdata. It applies necessary patches, standardises variables, and applies cross-sectional weights to construct the national macro-aggregates.
- **`VERIFICATION EUROSTAT`**: An automated validation script that queries the official Eurostat API to download official macro-aggregates and calculates the Mean Absolute Error (MAE) against our constructed dataset.

### B. Summary Statistics & Main Econometric Analysis
- **`TABLE 1 SUMMARY STATISTICS`**: Calculates and exports the summary statistics for the full unbalanced panel (Table 1).
- **`ECONOMETRIC MODEL`**: Contains the baseline one-way fixed effects models with 1-year lagged independent variables. It applies Arellano clustered standard errors and directly exports Table 2.

### C. Diagnostics & Robustness Checks (Requested during Peer Review)
- **`DISCOLL KRAAY STANDARD ERRORS`**: Estimates the robustness check models using Two-Way Fixed Effects (Country & Year FE), executes Pesaran CD diagnostic tests, performs a sensitivity analysis on lag structures (`maxlag = 1, 2, 3`) for Driscoll-Kraay standard errors, and robustly exports Table A3.
- **`DIAGNOSTICS ECONOMETRICS TESTS`**: Executes formal diagnostic tests for heteroskedasticity (Breusch-Pagan) and serial correlation (Breusch-Godfrey/Wooldridge).
- **`DIAGNOSTICS HAUSMAN VIFS`**: Executes the Hausman specification test and calculates the Variance Inflation Factor (VIF) to rule out multicollinearity.
- **`ROBUSTNESS FAILED GMM`**: Provided for absolute transparency. This script contains the initially attempted two-step System GMM dynamic panel model, which was ultimately abandoned due to severe instrument proliferation.

### D. Appendix Tables
- **`TABLE A1 CORRELATION MATRIX`**: Generates and exports the Pearson Correlation Matrix ensuring no pairwise correlation exceeds multicollinearity thresholds (Table A1).
- **`TABLE A2 DATA COVERAGE`**: Generates and exports the unbalanced panel coverage map and observations (T) per country (Table A2).

## 5. Instructions for Use
1. Save all scripts and the `Thesis_Final_Panel_Dataset_Bulletproof.csv` file in the same local directory.
2. Set that directory as your Working Directory in R (`setwd("path/to/folder")`) or open the folder as an RStudio Project.
3. You can execute any script from sections B, C, and D directly, as they seamlessly load the provided `.csv` dataset using relative paths.
4. The tables (Table 1, Table 2, A1, A2, A3) will be automatically exported to your working directory as formatted `.doc` files.

## 6. Contact
For any questions regarding the code or the dataset, please contact the corresponding author.
