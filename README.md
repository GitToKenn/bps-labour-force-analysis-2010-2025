# 📊 BPS Labour Force – August Time Series Analysis (2010–2024)

This project is inspired by a Tableau course exercise on **unemployment time-series visualisation**, adapted to the Indonesian context.  
Instead of using U.S. Bureau of Labor Statistics data, here we process and visualise the **Badan Pusat Statistik (BPS) Labour Force August releases** from **2010–2024**.  

The goal is to create a structured, reproducible pipeline that cleans BPS raw CSVs and prepares them for **time-series analysis and visualisation**. With the cleaned data, we can replicate and extend charts such as:

- 📈 Unemployment trends by **age group**  
- 🔎 Focused view on **25–34 year olds**, often most sensitive to labour market shocks  
- 📉 Time-series highlighting major events (e.g., COVID-19 impact, post-pandemic recovery)  

🛠️ **Status**: cleaning labour force data & rates; Tableau visualisation in progress  
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
  - `02_data_cleaning_lf.ipynb` – Clean LF dataset  
- [data/](data/) – Datasets  
  - `raw/` – Original BPS files (ignored)  
  - `clean/` – Cleaned outputs  
    - `tp_cleaned.xlsx` – Population 15+  
    - `lf_cleaned.xlsx` – Labour force  
- [dashboard/](dashboard/) – Tableau (ignored until final)
- [.gitignore](.gitignore) – Ignore raw + temp files


--- 

### 🗂️ Folder Tree

```
root/
├── README.md
├── .gitignore
├── data/
│   ├── raw/        (excluded)
│   └── clean/
│       ├── tp_cleaned.xlsx
│       └── lf_cleaned.xlsx
├── notebooks/
│   ├── 01_data_cleaning_tp.ipynb
│   ├── 02_data_cleaning_lf.ipynb
│   └── 03_metrics.ipynb   (planned)
└── dashboard/
    └── lfpr_unemployment_experiment.twb (ignored until final)
```
---


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

Two categories of cleaned datasets are produced:

- **Labour Force (lf)**  
  - ✅ `bps_lf_detail_2010_2025_<timestamp>.csv`  
    - Age group breakdowns (no “Total”)  
    - Columns: `Age Group, February, August, Year`  
  - ✅ `bps_lf_total_2010_2025_<timestamp>.csv`  
    - Yearly totals only  
    - Columns: `Year, February, August`  

- **Total Population (tp)**  
  - ✅ `bps_tp_detail_2010_2025_<timestamp>.csv`  
    - Age group breakdowns (no “Total”)  
    - Columns: `Age Group, February, August, Year`  
  - ✅ `bps_tp_total_2010_2025_<timestamp>.csv`  
    - Yearly totals only  
    - Columns: `Year, February, August`  

---

## 🛡️ Disclaimer

- This project uses **publicly available BPS data** from official August Labour Force releases.  
- Original raw CSVs are excluded from the repository due to licensing and storage.  
- Cleaning procedures (dropping rows, renaming, numeric conversion) are documented in notebooks.  
- Official source links:  
  - [Labor Force (LF) by Age Group, 2025](https://www.bps.go.id/en/statistics-table/2/Njk4IzI=/labor-force--lf--by-age-group.html)  
  - [Total Population of Age 15 and above by Age Group, 2025](https://www.bps.go.id/en/statistics-table/2/NzE1IzI=/total-population-of-age-15-and-above-by-age-group.html)   