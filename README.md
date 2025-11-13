## 🦠 Global COVID-19 EDA Project [COVID-19 Global Analysis (Kaggle: covid_19_clean_complete.csv)]

## Summary:
This project performs an end-to-end analysis of global COVID-19 trends using the Kaggle dataset covid_19_clean_complete.csv. The workflow includes ingestion into a SQLite database, SQL-based analytics using window functions, computation of daily and cumulative metrics, region-wise comparisons, visualization of time-series trends, correlation analysis, and statistical hypothesis testing (ANOVA) on country-level Case Fatality Rates (CFR).
The project demonstrates the combined use of SQL, Python, statistics, and visualization to extract meaningful insights from a real-world epidemiological dataset.

## 📊 Dataset Overview

The dataset contains global daily COVID-19 records from January 2020 to July 2020, including:

Country/Region|
Latitude, Longitude|
Date|
Confirmed cases (cumulative)|
Deaths (cumulative)|
Recovered (cumulative)|
Active cases (cumulative)|
WHO Region

It covers 187 countries, enabling country-level and region-level comparisons.

## 🧠 Key Analytical Decisions

Final case counts are computed using MAX() because the dataset stores cumulative daily values.
Daily new cases are computed using SQL window functions:
Confirmed - LAG(Confirmed) OVER (PARTITION BY country ORDER BY Date)
Region-level daily totals use SUM() across all countries in the region.

Case Fatality Rate (CFR) and Case Recovery Rate (CRR) are calculated using final totals:
ROUND(MAX(Deaths) * 100.0 / (MAX(Confirmed), 2)


## 🚀 Project Highlights & Key Findings
1. Countries with Highest Daily New Cases

Using window functions, the project identifies countries with the most severe one-day spikes.
In this dataset, the United Kingdom shows unusually large spikes due to reporting adjustments.

2. Global CFR (Case Fatality Rate) Insights

Highest CFR values appear in Yemen, UK, Italy, Belgium, reflecting a combination of limited reporting, overwhelmed healthcare systems, and demographic factors.
Lower CFR values appear across Africa and South-East Asia, partly due to younger populations and differing testing strategies.

3. WHO Region Trends

Americas region shows the highest cumulative cases and deaths.
Europe shows higher fatality ratios, consistent with early pandemic waves.
Eastern Mediterranean and South-East Asia show strong recovery rates in the dataset.

4. Correlation Analysis

Confirmed cases vs Deaths: Strong positive correlation
Deaths vs Recovered: Also highly correlated
The virus spreads exponentially; highly infected countries show proportional increases in deaths and recoveries.

5. ANOVA Statistical Test (CFR by WHO Region)
   
ANOVA conducted on country-level CFR grouped by WHO regions reveals:
p ≈ 0.0088 (significant) when all countries are included
p ≈ 0.0539 (not significant) when countries with very low case counts are filtered
This demonstrates how small countries with extreme CFR values influence statistical significance.

📝 Notes & Limitations

Some countries (e.g., United Kingdom) stopped reporting recovery numbers → CRR becomes unreliable.
COVID-19 data includes reporting delays and mass backlog updates, which are preserved because they represent real events.
The dataset ends in July 2020, covering only the initial pandemic waves.
Results may not represent later pandemic dynamics.
