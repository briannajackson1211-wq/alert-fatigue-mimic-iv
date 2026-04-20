---

## Data Access

This project uses **MIMIC-IV v3.0**, a publicly available critical care database 
developed by the MIT Laboratory for Computational Physiology.

To access the data:

1. Create an account at https://physionet.org
2. Complete the required CITI training course
3. Sign the data use agreement for MIMIC-IV
4. Download the following tables:
   - `hosp/patients.csv`
   - `hosp/admissions.csv`
   - `hosp/prescriptions.csv.gz`
   - `icu/icustays.csv`
   - `hosp/labevents.csv.gz`

Full documentation: https://physionet.org/content/mimiciv/

---

## How to Reproduce This Analysis

### Requirements

- R 4.x or higher
- RStudio (recommended)
- The following R packages:

```r
install.packages(c(
  "data.table",
  "MASS",
  "ggplot2",
  "lubridate",
  "tidyr",
  "scales",
  "knitr",
  "kableExtra",
  "broom",
  "dplyr",
  "duckdb"
))
```

### Steps

1. Clone or download this repository
2. Obtain MIMIC-IV access and download the required tables
3. Open `Evaluating-Alert-Fatigue-Codebook.Rmd` in RStudio
4. Update the file paths in the `load-data` chunk to match your local directory:

```r
cohort <- fread("YOUR/PATH/TO/mimic_icustay_cohort_final.csv")
prescriptions <- fread("YOUR/PATH/TO/prescriptions.csv.gz")
```

5. Knit the document to reproduce all tables, figures, and model outputs

---

## Statistical Approach

- **Model:** Negative binomial regression
- **Outcome variables:** Medication orders per day, laboratory events per day, 
  total CDS-triggering events per day
- **Predictors:** ICU unit type, patient age, patient gender
- **Offset:** Log-transformed ICU length of stay
- **Software:** R 4.x with MASS package (glm.nb function)
- **Overdispersion confirmed:** Variance-to-mean ratios ranging from 119 to 1,178; 
  likelihood ratio test χ² = 8,224,010, p < 0.0001

---

## Citation

If you use this code or framework in your own research please cite:

Jackson, B. D. (2026). *Evaluating alert fatigue in clinical decision support 
systems* [Practicum report]. North Carolina Agricultural and Technical 
State University.

---

## Contact

Brianna D. Jackson  
North Carolina Agricultural and Technical State University
