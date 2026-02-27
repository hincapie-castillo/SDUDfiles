# Medicaid State Drug Utilization & Enrollment Data

Standardized CSV files for Medicaid drug utilization analysis, prepared for use with the public dashboard

## Data Sources

### State Drug Utilization Data (SDUD)
- **Source:** [data.medicaid.gov](https://data.medicaid.gov) and [download.medicaid.gov](https://download.medicaid.gov)
- **Original publisher:** Centers for Medicare & Medicaid Services (CMS)
- **Description:** Quarterly prescription drug utilization reported by state Medicaid agencies under the Medicaid Drug Rebate Program. Includes state, drug name, NDC, number of prescriptions, and dollars reimbursed.
- **Coverage:** 2016–2025 (one file per year)
- **Documentation:** [SDUD FAQ](https://www.medicaid.gov/medicaid/prescription-drugs/state-drug-utilization-data/state-drug-utilization-data-faq)

### Medicaid Enrollment (MBES)
- **Source:** [data.medicaid.gov](https://data.medicaid.gov/dataset/6c114b2c-cb83-559b-832f-4d8b06d6c1b9)
- **Original publisher:** Centers for Medicare & Medicaid Services (CMS)
- **Description:** Total Medicaid Enrollees reported quarterly through the Medicaid Budget and Expenditure System (MBES/CBES). State-reported unduplicated count of individuals enrolled at any time during each month within the quarterly reporting period.
- **Coverage:** 2014–2022 (quarterly, end-of-quarter months only)
- **Documentation:** [MBES Enrollment Page](https://www.medicaid.gov/medicaid/national-medicaid-chip-program-information/medicaid-chip-enrollment-data/medicaid-enrollment-data-collected-through-mbes)

## Files

| File | Description | Key Columns |
|------|-------------|-------------|
| `sdud_2016.csv` – `sdud_2025.csv` | Drug utilization by state, quarter, NDC | `utilization_type`, `state`, `ndc`, `product_name`, `year`, `quarter`, `number_of_prescriptions`, `total_amount_reimbursed`, `units_reimbursed` |
| `enrollment.csv` | Total Medicaid Enrollment by state and quarter | `report_period` (YYYYMM), `quarter_label` (e.g. 2016-Q1), `state` (abbreviation), `enrollment` |

## Column Definitions

### SDUD Files
| Column | Description |
|--------|-------------|
| `utilization_type` | FFSU (Fee-for-Service) or MCOU (Managed Care) |
| `state` | Two-letter state abbreviation |
| `ndc` | 11-digit National Drug Code |
| `product_name` | Drug product name |
| `year` | Calendar year |
| `quarter` | Calendar quarter (1–4) |
| `number_of_prescriptions` | Number of prescriptions reimbursed |
| `total_amount_reimbursed` | Total dollar amount reimbursed (pre-rebate) |
| `units_reimbursed` | Number of units reimbursed |

### Enrollment File
| Column | Description |
|--------|-------------|
| `report_period` | YYYYMM format (quarter-end month: 03, 06, 09, 12) |
| `quarter_label` | Human-readable label (e.g. 2016-Q1) |
| `state` | Two-letter state abbreviation |
| `enrollment` | Total Medicaid Enrollees (unduplicated count) |

## Quarter-to-Reporting Period Mapping

SDUD quarters map to MBES enrollment as follows:

| SDUD Quarter | Last Month | `report_period` |
|-------------|------------|-----------------|
| Q1 (Jan–Mar) | March | YYYY03 |
| Q2 (Apr–Jun) | June | YYYY06 |
| Q3 (Jul–Sep) | September | YYYY09 |
| Q4 (Oct–Dec) | December | YYYY12 |

## Important Notes

- **Pre-rebate amounts:** Dollar amounts in SDUD are pre-rebate and do not reflect manufacturer rebates paid to states.
- **Suppressed values:** Cells with fewer than 11 prescriptions are suppressed by CMS for privacy. These appear as missing values.
- **Enrollment source:** Enrollment counts are from MBES (CMS-64 quarterly expenditure reports), not the Performance Indicator dataset. MBES counts include individuals enrolled in limited benefit plans. See [CMS methodology notes](https://www.medicaid.gov/medicaid/national-medicaid-chip-program-information/medicaid-chip-enrollment-data/medicaid-enrollment-data-collected-through-mbes) for details.
- **State "XX":** In SDUD, state code "XX" represents national totals. These are excluded in per-state analyses.

## Data Preparation

Files were prepared using a Python script run in Google Colab. The script downloads raw data from CMS APIs and bulk CSV endpoints, standardizes column names, converts data types, filters to relevant columns, and exports clean CSVs. The preparation script is available upon request.

## Suggested Citation

Centers for Medicare & Medicaid Services. State Drug Utilization Data [dataset]. Available from: https://data.medicaid.gov. Accessed [date].

Centers for Medicare & Medicaid Services. Medicaid Enrollment Data Collected Through MBES [dataset]. Available from: https://data.medicaid.gov/dataset/6c114b2c-cb83-559b-832f-4d8b06d6c1b9. Accessed [date].

## License

Original data are U.S. government works in the public domain. This repository provides reformatted copies for analytical convenience. No restrictions on reuse.
