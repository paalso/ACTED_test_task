# ACTED HNMU Data Officer — Test Assignment

This project contains my solution to the **HNMU (Humanitarian Needs and Monitoring Unit) Data Officer Test Assignment**  of **ACTED/REACH**, which consists of three parts:
data cleaning & preprocessing, data analysis, and dashboard creation.

All scripts, input data, outputs, and the dashboard are included in this repository.

## 🔧 1. Data Cleaning & Preprocessing (Python)

All steps are implemented in [`notebooks/task.ipynb`](https://github.com/paalso/ACTED_test_task/blob/main/notebooks/task.ipynb):

### 1.1 Remove incomplete surveys

- Records with missing critical fields were removed.

- Sample size requirements (≥159 interviews per oblast) were checked.

### 1.2 Logic check for disability vs household size

- Implemented validation rule from task description.

- Records failing the check had their disability fields set to NA (as required).

### 1.3 Total income per capita

- Calculated using total household income divided by household size.

- Result stored as new variable `income_per_capita`.

## 📊 2. Data Analysis (Python)

### 2.1 Average income per capita + margin of error

- Grouped by oblast (`oblast`).

- Calculated:

  - mean income per capita

  - standard error

  - margin of error at 95% confidence

### 2.2 Livelihoods LSG (levels 1–4 or NA)

- Rules taken from *Livelihoods_LSG.xlsx*  .

Three dimensions calculated:

Income sources (`lsg_income_sources`)

Total income per capita (`lsg_income_per_capita`)

Livelihoods coping strategies (`lsg_lcsi`)

Final `livelihoods_lsg` = maximum of the three levels;
if any dimension is NA → full result = NA.

## 📈 3. Dashboard (Power BI)

The dashboard file is located at:

`dashboard/dashboard.pbix`

The dashboard includes:

### 3.1 Top-5 oblasts by average income per capita

Bar chart based on aggregated results from task 2.1.

### 3.2 Distribution of Livelihoods LSG (1–4)

Donut or bar chart showing percentage of households at each level.

### 3.3 Disability filter

A slicer based on `disability_count`, with two options:

Households with disability (responses starting with "yes")

- ***No disability***
- ***With disability***

### 3.4 Respondent count by oblast (map)

Shape map of Ukraine showing number of respondents per oblast.
Includes custom TopoJSON file: *data/Ukraine-regions-ua*.

The result dashboard [`reports/dashboard.pbix`](https://github.com/paalso/ACTED_test_task/blob/main/reports/dashboard.pbix)

![Dashboard preview](https://github.com/paalso/ACTED_test_task/blob/main/reports/dashboard.jpg)

## The dataset columns description

| Dataset column | Description |
| --- | --- |
| start | Timestamp when the interview started |
| end | Timestamp when the interview ended. |
| date_survey | Date of the survey |
| A_2_consent | Consent to participate ("yes"). |
| oblast_kiis | Administrative region (oblast) where the interview was conducted |
| raion_kiis | District (raion) within the oblast |
| A_5_resp_age | Age of the respondent (numeric) |
| A_18_resp_hoh | Whether the respondent is the head of household (yes/no) |
| A_19_resp_hoh_behalf | Notes if the interview is conducted on behalf of the head of household |
| B_2_hh_size | Total number of people in the household |
| B_13_disability_regist | Whether the household includes members with officially registered disabilities |
| B_13_disability_regist/yes_group_1 | Household has a member in disability group 1 |
| B_13_disability_regist/yes_group_2 | Household has a member in disability group 2 |
| B_13_disability_regist/yes_group_3 | Household has a member in disability group 3 |
| B_13_disability_regist/yes_but_unsure_which_group | Disability present but group unknown |
| J_27_income_sources | List of all income sources selected by the household (multi-select) |
| J_27_income_sources/salaried_work | Household receives salaried work income |
| J_27_income_sources/casual_or_daily_labour | Household receives casual/daily labor income |
| J_27_income_sources/income_from_own_business_or_regular_trade | Household receives business income |
| J_27_income_sources/income_from_own_production | Household receives income from own production |
| J_27_income_sources/idp_benefits | Household receives IDP benefits |
| J_27_income_sources/pension | Household receives pension |
| J_27_income_sources/other_government_social_benefits_or_assistance | Household receives other government assistance |
| J_27_income_sources/income_from_rent | Household receives rental income |
| J_27_income_sources/money_transfers_from_abroad_from_family_and_friends | Household receives remittances from abroad |
| J_27_income_sources/humanitarian_aid | Household receives humanitarian aid |
| J_29_inc_salary | Numeric salary income (UAH) |
| J_30_inc_labor | Numeric casual/daily labor income (UAH) |
| J_31_inc_business | Numeric business income (UAH) |
| J_32_inc_produc | Numeric income from own production (UAH) |
| J_33_inc_idp | Numeric IDP benefits income (UAH) |
| J_34_inc_pension | Numeric pension income (UAH) |
| J_35_inc_benefit | Numeric other benefits income (UAH) |
| J_36_inc_rent | Numeric rental income (UAH) |
| J_37_inc_remittance | Numeric remittance income (UAH) |
| J_38_inc_aid | Numeric humanitarian aid income (UAH) |
| fsl_lcsi_stress1 | Stress-level coping strategy indicator 1 |
| fsl_lcsi_stress2 | Stress-level coping strategy indicator 2 |
| fsl_lcsi_stress3 | Stress-level coping strategy indicator 3 |
| fsl_lcsi_stress4 | Stress-level coping strategy indicator 4 |
| fsl_lcsi_crisis1 | Crisis-level coping strategy indicator 1 |
| fsl_lcsi_crisis2 | Crisis-level coping strategy indicator 2 |
| fsl_lcsi_crisis3 | Crisis-level coping strategy indicator 3 |
| fsl_lcsi_emergency1 | Emergency-level coping strategy indicator 1 |
| fsl_lcsi_emergency2 | Emergency-level coping strategy indicator 2 |
| fsl_lcsi_emergency3 | Emergency-level coping strategy indicator 3 |
| enum_id_msna_cati | Enumerator ID / CATI operator identifier |
| uuid | Unique ID for each survey submission |
| _index | Sequential record index from the original XLSForm |
