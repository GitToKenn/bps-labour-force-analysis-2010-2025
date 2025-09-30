# 📊 BPS Labour Force – August Time Series Analysis (2010–2024)

This project is inspired by a Tableau course exercise on **unemployment time-series visualisation**, adapted to the Indonesian context.  
Instead of using U.S. Bureau of Labor Statistics data, here we process and visualise the **Badan Pusat Statistik (BPS) Labour Force August releases** from **2010–2024**.  

The goal is to create a structured, reproducible pipeline that cleans BPS raw CSVs and prepares them for **time-series analysis and visualisation**. With the cleaned data, we can replicate and extend charts such as:

- 📈 Unemployment trends by **age group**  
- 🔎 Focused view on **25–34 year olds**, often most sensitive to labour market shocks  
- 📉 Time-series highlighting major events (e.g., COVID-19 impact, post-pandemic recovery)  

🛠️ **Status**: combined labour force variables (Work, Unemp, Total, Emp Rate) into unified dataset; preparing Tableau dashboard for visualisation
🔒 **Repo**: Public 

---

## 📌 Project Goals

- **Reproduce Tableau-style time series** of labour force participation and unemployment using BPS data (2010–2025)  
- Build a **reliable cleaning pipeline** for BPS CSV quirks: header rows, unnamed columns, totals  
- Standardise column names and convert values to numeric for time-series analysis  
- Produce **clean datasets**:  
  - Population 15+ (TP)  
  - Labour Force (LF: employed, unemployed, total)  
- Derive key metrics: **LFPR, Unemployment Rate (TPT), Employment-to-Population Ratio (EPR)**  
- Export cleaned tables for reuse in **Python, R, or Tableau**  
- Create Tableau dashboards for **age-group trends** and **event-driven patterns** (e.g., COVID-19 impact)  

---

## 📂 Project Structure

- [README.md](README.md) – Project overview  
- [notebooks/](notebooks/) – Jupyter notebooks  
  - `01_data_cleaning_tp.ipynb` – Clean TP dataset  
  - `02_data_cleaning_lf_work.ipynb` – Clean LF_work (employed)  
  - `03_data_cleaning_lf_unemp.ipynb` – Clean LF_unemp (unemployment)  
  - `04_data_cleaning_lf_total.ipynb` – Clean LF_total (labour force total)  
  - `05_data_cleaning_lf_emp_rate.ipynb` – Clean LF_emp_rate (employment share)  
- [data/](data/) – Datasets  
  - `raw/` – Original BPS files (ignored)  
  - `clean/` – Cleaned outputs (CSV, timestamped)  
    - `bps_tp_detail_2010_2025_<timestamp>.csv`  
    - `bps_tp_total_2010_2025_<timestamp>.csv`  
    - `bps_lf_work_detail_2010_2025_<timestamp>.csv`  
    - `bps_lf_work_total_2010_2025_<timestamp>.csv`  
    - `bps_lf_unemp_detail_2010_2025_<timestamp>.csv`  
    - `bps_lf_unemp_total_2010_2025_<timestamp>.csv`  
    - `bps_lf_total_detail_2010_2025_<timestamp>.csv`  
    - `bps_lf_total_total_2010_2025_<timestamp>.csv`  
    - `bps_lf_emp_rate_detail_2010_2025_<timestamp>.csv`  
    - `bps_lf_emp_rate_total_2010_2025_<timestamp>.csv`  
- [dashboard/](dashboard/) – Tableau experiments (ignored until final)  
- [.gitignore](.gitignore) – Ignore raw + temp files  


--- 

### 🗂️ Folder Tree

```
root/
├── README.md
├── .gitignore
├── data/
│   ├── raw/         (excluded)
│   └── clean/
│       ├── bps_tp_detail_2010_2025_<timestamp>.csv
│       ├── bps_tp_total_2010_2025_<timestamp>.csv
│       ├── bps_lf_work_detail_2010_2025_<timestamp>.csv
│       ├── bps_lf_work_total_2010_2025_<timestamp>.csv
│       ├── bps_lf_unemp_detail_2010_2025_<timestamp>.csv
│       ├── bps_lf_unemp_total_2010_2025_<timestamp>.csv
│       ├── bps_lf_total_detail_2010_2025_<timestamp>.csv
│       ├── bps_lf_total_total_2010_2025_<timestamp>.csv
│       ├── bps_lf_emp_rate_detail_2010_2025_<timestamp>.csv
│       └── bps_lf_emp_rate_total_2010_2025_<timestamp>.csv
├── notebooks/
│   ├── 01_data_cleaning_tp.ipynb
│   ├── 02_data_cleaning_lf_work.ipynb
│   ├── 03_data_cleaning_lf_unemp.ipynb
│   ├── 04_data_cleaning_lf_total.ipynb
│   └── 05_data_cleaning_lf_emp_rate.ipynb
└── dashboard/
    └── lfpr_unemployment_experiment.twb (ignored until final)
```

---

## 📊 Dataset Overview

- Source: Badan Pusat Statistik (BPS) – Labour Force August releases  
- Coverage: **2010–2025** (based on data available from BPS up to **February 2025**)  
- Observations: population aged 15+ segmented by age groups  
- Format: CSV, annual (August release)  

---

## 🧹 Cleaning & Processing Summary

- **Removed top 3 header rows** in each CSV  
- **Dropped unused columns** (e.g., `"Unnamed: 3"`)  
- **Standardised column names**:  
  - `Unnamed: 1` → `February`  
  - `Unnamed: 2` → `August`  
  - `year` → `Year`  
  - `Age group` → `Age Group`  
- **Cleaned numeric fields**: removed dots/commas, converted to `Int64`  
- **Handled missing values**: August values set to `NaN` where unavailable  
- **Split datasets**:  
  - **Detail** → all age groups except `"Total"`  
  - **Total** → yearly `"Total"` rows only  
- **Concatenated yearly files** into two master DataFrames (`detail` & `total`)  
- **Exported** final datasets as timestamped CSVs  

---

## ✨ Outputs

Cleaned datasets (2010–2025) are produced in two groups:

- **Labour Force (LF)**  
  - `bps_lf_work_detail_<timestamp>.csv` / `bps_lf_work_total_<timestamp>.csv`  
  - `bps_lf_unemp_detail_<timestamp>.csv` / `bps_lf_unemp_total_<timestamp>.csv`  
  - `bps_lf_total_detail_<timestamp>.csv` / `bps_lf_total_total_<timestamp>.csv`  
  - `bps_lf_emp_rate_detail_<timestamp>.csv` / `bps_lf_emp_rate_total_<timestamp>.csv`  

- **Total Population (TP)**  
  - `bps_tp_detail_<timestamp>.csv` / `bps_tp_total_<timestamp>.csv`  

Each dataset contains either **detail** (age group breakdown, no “Total”) or **total** (yearly aggregates) with consistent columns:  
- Detail → `Age Group, February, August, Year`  
- Total → `Year, February, August`  

---

## 🛡️ Disclaimer

- This project uses **publicly available BPS data** from official August Labour Force releases.  
- Original raw CSVs are excluded from the repository due to licensing and storage.  
- Cleaning procedures (dropping rows, renaming, numeric conversion) are documented in notebooks.  
- Official source links:  
  - [Labor Force (LF) by Age Group, 2025](https://www.bps.go.id/en/statistics-table/2/Njk4IzI=/labor-force--lf--by-age-group.html)  
  - [Total Population of Age 15 and above by Age Group, 2025](https://www.bps.go.id/en/statistics-table/2/NzE1IzI=/total-population-of-age-15-and-above-by-age-group.html)   