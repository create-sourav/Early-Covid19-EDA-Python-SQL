### 🦠 Global COVID-19 EDA Project

#### COVID-19 Global Analysis (Kaggle: covid_19_clean_complete.csv)

### 📌 Summary

This project performs an end-to-end exploratory data analysis (EDA) of global COVID-19 trends using the Kaggle dataset **covid_19_clean_complete.csv**.

The workflow includes:
- Ingesting the dataset into a **SQLite database**
- Conducting **SQL analytics** using window functions
- Computing **daily and cumulative metrics**
- Performing **country-level and WHO-region-level** comparisons
- Creating **visualizations** for trends and correlations
- Running **statistical tests (ANOVA)** on Case Fatality Rates (CFR)

This project demonstrates combined expertise in **SQL, Python, statistical analysis, and data visualization**, applied to a real-world epidemiological dataset.

### 📊 Dataset Overview

The dataset contains global daily COVID-19 records from **January 2020 to July 2020**, with the following columns:

- **Country/Region**
- **Latitude, Longitude**
- **Date**
- **Confirmed cases (cumulative)**
- **Deaths (cumulative)**
- **Recovered (cumulative)**
- **Active cases (cumulative)**
- **WHO Region**

The dataset covers **187 countries**, allowing for detailed time-series and regional analysis.

### 🧠 Key Analytical Decisions

#### ✔ Cumulative Metrics (MAX)
Final totals per country/region use:
```sql
MAX(Confirmed), MAX(Deaths), MAX(Recovered)
```

#### ✔ Daily New Cases (Window Function)
Daily new infections are computed using:
```sql
Confirmed - LAG(Confirmed) OVER (PARTITION BY country ORDER BY Date)
```

#### ✔ Region-Level Daily Aggregation
Daily trends across WHO regions use:
```sql
SUM(Confirmed) GROUP BY region, Date
```

#### ✔ CFR & CRR Calculation
**Case Fatality Rate (CFR):**
```sql
ROUND(MAX(Deaths) * 100.0 / NULLIF(MAX(Confirmed), 0), 2)
```

**Case Recovery Rate (CRR):**
```sql
ROUND(MAX(Recovered) * 100.0 / NULLIF(MAX(Confirmed), 0), 2)
```

### 🚀 Project Highlights & Key Findings

#### 1️⃣ Countries With Highest Daily New Cases
- Window functions reveal significant one-day spikes
- **United Kingdom** shows unusually large jumps due to reporting adjustments and data corrections

#### 2️⃣ Global CFR (Case Fatality Rate) Insights
**Highest CFRs** appear in Yemen, UK, Italy, Belgium → linked to overwhelmed healthcare systems, limited testing, and demographic vulnerabilities.

**Lower CFRs** are seen in Africa and South-East Asia, influenced by:
- Younger populations
- Different surveillance strategies
- Under-reporting of milder cases

#### 3️⃣ WHO Region Trends
- **Americas** show the highest cumulative cases and deaths
- **Europe** exhibits higher fatality ratios
- **Eastern Mediterranean and South-East Asia** show strong recovery rates
- **Africa** shows lower fatality rates but also limited testing

#### 4️⃣ Correlation Analysis
- **Confirmed vs Deaths:** Strong positive correlation
- **Deaths vs Recovered:** Also strongly correlated
- Indicates the exponential spread pattern of the virus
- Countries with high infections tend to show higher deaths and recoveries

#### 5️⃣ ANOVA Statistical Test (CFR by WHO Region)
ANOVA performed on country-level CFR grouped by WHO regions shows:
- **p ≈ 0.0088** (significant) → When all countries are included
- **p ≈ 0.0539** (not significant) → After filtering out countries with very low case counts

This demonstrates that:
- Small-population countries with extreme CFR values strongly influence statistical significance
- When outlier regions are removed, CFR differences between WHO regions become statistically weaker

### 📝 Notes & Data Limitations

- Some countries (e.g., **United Kingdom**) stopped reporting recovery data → CRR becomes unreliable or zero
- Data contains **reporting lags and mass backlog uploads**, especially for Confirmed and Deaths
- Dataset ends in **July 2020**, representing only early pandemic waves
- Regional comparisons may be affected by:
  - Different healthcare systems
  - Inconsistent testing strategies
  - Political and reporting biases

### 🛠️ Technologies Used

- **Python** (pandas, numpy, matplotlib, seaborn, scipy)
- **SQL** (SQLite, window functions, aggregations)
- **Statistical Analysis** (ANOVA, correlation analysis)
- **Data Visualization** (time-series plots, heatmaps, bar charts)

### 🎯 Future Enhancements

- Extend analysis to include **vaccination data**
- Incorporate **mobility trends** and **policy interventions**
- Add **predictive modeling** (ARIMA, Prophet)
- Create **interactive dashboards** using Plotly/Dash

### 👤 Author

**[Sourav Mondal]**

### 🙏 Acknowledgments

- Dataset: Kaggle COVID-19 Dataset
- The global health community for data collection efforts
