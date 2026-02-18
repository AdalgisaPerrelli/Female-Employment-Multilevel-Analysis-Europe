# Female Employment in Europe: A Multilevel Logistic Regression Analysis

This repository contains the code and material for my bachelor thesis on female employment in Europe. 
The study analyses the employment status of women aged 20–49 in Italy, France and Germany using EU Labour Force Survey (EU‑LFS) 2021 microdata and multilevel logistic regression models.

---

## Research aim

The goal is to explain differences in female employment rates across Italy, France and Germany in terms of key individual and contextual characteristics such as age, number and age of children, household composition, education, country of birth, citizenship and regional socio‑economic indicators.

---

## Data

- **Source**: EU Labour Force Survey (EU‑LFS), year 2021 (Eurostat).
- **Population**: women aged 20–49 living in Italy, France and Germany.
- **Sampling weights**: all descriptive statistics and models use survey weights to recover population‑level estimates.

Main variables include:

- **EMPSTAT** – binary outcome: 0 = not employed, 1 = employed.  
- **DEGURBA** – degree of urbanisation of the area of residence.  
- **AGEGRP** – five‑year age groups (20–24, 25–29, …, 45–49).  
- **HHNBCH0TO2, HHNBCH3TO5, HHNBCH6TO8, HHNBCH9TO17** – number of children in different age ranges in the household.  
- **HHNBOLD** – number of household members aged 65+.  
- **HHNBADOUTLF** – number of adults out of the labour force in the household.  
- **HHPARENT, HHPARTNR** – presence of parents and partner in the household.  
- **COUNTRYBmod, CITIZENSHIPmod** – grouped country of birth and citizenship.  
- **YEARESIDmod** – grouped years of residence in the country.  
- **HATLEVELmod, HATFIELDmod** – highest educational level and field (grouped).  
- **REGION2D** – region of residence (NUTS2 for Italy and France, NUTS1 for Germany).  
- **COEFFY** – survey weight.  

Regional‑level variables (level‑2 covariates), merged by region:

- **EDUTER** – share of women 25–64 with tertiary education.  
- **TFT** – total fertility rate (average number of children per woman).  
- **REDFAM** – average family income.  
- **UNIFAM, SPOSFAM, MAMFAM, MULTIFAM** – regional indicators of family structure.

---

## Methods

The empirical strategy relies on multilevel (mixed‑effects) logistic regression models.

### 1. Descriptive analysis

- Weighted descriptive statistics of the main variables.
- Weighted employment rates by:
  - age group
  - number and age of children
  - presence of partner
  - country of birth and citizenship
  - education level
  - years of residence in the country.

### 2. Model specification

For each country, a sequence of models is fitted:

1. **Initial multilevel logistic model**  
   - Outcome: `EMPSTAT` (employed vs not employed).  
   - Level‑1 predictors: individual characteristics (DEGURBA, AGEGRP, child counts, household composition, education, migration background, years of residence, etc.).  
   - Level‑2 predictors: regional covariates (EDUTER, TFT, REDFAM, UNIFAM, SPOSFAM, MAMFAM, MULTIFAM).  
   - Random intercept for `REGION2D`.

2. **Reduced model**  
   - Non‑significant or collinear variables are removed after significance tests, collinearity checks and separation diagnostics.
   - Final “parsimonious” models are selected using likelihood‑ratio tests and information criteria (AIC/BIC).

Effects are interpreted in terms of odds ratios (exponentiated fixed effects), focusing on how covariates are associated with the probability of being employed.

---

## Main findings (brief)

Some of the key empirical findings, at a high level, are:

- In 2021, the employment rate of women aged 20–49 is substantially lower in Italy than in France and Germany.  
- In all three countries, the presence and number of young children (especially aged 0–5) are strongly associated with lower employment probabilities.  
- Higher education levels are positively associated with female employment, with large gaps between low and tertiary education.  
- Migration‑related variables (citizenship, years of residence) play a stronger role in Italy than in France and Germany.  
- Regional‑level indicators such as tertiary education share and fertility help explain cross‑regional differences in employment probabilities.

For full details, refer to the thesis document and the R Markdown script.

---

## Files

- `tesi-ITALIA_PERRELLI.Rmd`  
  R Markdown file with the full data preparation, variable recoding, descriptive statistics and multilevel logistic regression models (and structure for the other countries).

- `ElaboratoTesiTriennale_PERRELLI_VersioneDefinitiva.pdf`  
  Final thesis document (in Italian) describing the context, data, methodology, results and conclusions.

- `data/` *(not included)*  
  Folder where you should place the EU‑LFS microdata for Italy, France and Germany (not redistributed here due to Eurostat licence restrictions). File names and paths must be adapted in the R Markdown accordingly.

- `output/` *(optional)*  
  Folder for saving model outputs, tables and figures generated by the R Markdown.

---

## Software and packages

The analysis is conducted in **R**, mainly using:

- `Hmisc`, `psych`  
- `funModeling`, `VIM`  
- `plyr`, `dplyr`, `reshape2`  
- `skimr`  
- `ggplot2`, `coefplot`, `corrgram`, `lattice`  
- `lme4`, `lmerTest`, `mgcv`  
- `performance`, `lmtest`, `caret`  
- `survey`  
- `readxl`  
- `parallel`, `boot`, `compiler`

To install the packages in R:

```r
install.packages(c(
  "Hmisc", "psych", "funModeling", "plyr", "dplyr", "skimr",
  "ggplot2", "lme4", "lmerTest", "performance", "caret",
  "readxl", "survey", "VIM", "coefplot", "mgcv", "lmtest",
  "GGally", "reshape2", "compiler", "parallel", "boot", "lattice", "corrgram"
))
