# TVDE-Analysis

Exploratory performance and profitability analysis of a TVDE driver using Python, Pandas, and Matplotlib/Seaborn.

## 📌 Project Overview

This project focuses on a strategic analysis of real TVDE trip data collected over several months. Using Python for data processing and visualization, the main goal was to identify patterns in rentability, trip efficiency, and fuel cost impact across different days of the week, periods of the day, and pickup locations — providing a data-driven perspective on how to maximize net profit per trip.

---

## 🛠️ Tech Stack

- **Python / Pandas:** Used for data cleaning, transformation, merging datasets, and feature engineering.
- **Matplotlib / Seaborn:** Applied for data visualization and pattern discovery.
- **Excel:** Source format for raw trip data and fuel cost records.
- **Jupyter Notebook:** Used as the development and reporting environment.

---

## 📊 Key Analyses & Logic

### 1. Data Preparation & Cleaning
- Merged multiple monthly Excel files into a single DataFrame, using Power Query.
  - `Limpeza de dados.ipynb` — main data cleaning notebook where all raw data was processed, standardized, and prepared for analysis.
- Extracted temporal features such as `Period_of_Day` (Morning, Rush hour, Afternoon, Evening, Night) and `Week_Day` from the trip timestamp.
- Handled missing postal codes by mapping them to locality names, filling unmatched values as `Others`.
  - `CP_Grande_Porto.ipynb` — handles raw postal code data for Portugal, filtered to the Porto region only. Used to create the columns `nome_localidade_destino` and `nome_localidade_origem`. The main dataset contains sensitive information, so only the postal code was retained for the join.
- Calculated `Euro_Km` (revenue per km) as a normalized rentability metric per trip.
- Imported a separate fuel transaction dataset and calculated the **average fuel cost per km** by dividing total fuel spend by total kilometers driven.
- Applied this rate to each trip to estimate `Custo_Combustivel` and derive `Lucro_Liquido` (net profit per trip after fuel). This approach avoided data duplication issues that would arise from a direct date-based merge with multiple daily trips.

### 2. Rentability by Location
- Filtered locations with more than 10 trips to ensure statistical relevance.
- Ranked pickup locations by average `Euro_Km` to identify the most and least profitable origins.
- Cross-referenced with average trip duration to identify locations that are both fast and profitable.

### 3. Temporal Pattern Analysis
- Built a pivot table using `Week_Day` vs `Period_of_Day` with mean `Lucro_Liquido` to identify the best combinations of day and time.
- **Friday Afternoon** emerged as the top outlier (5.46€), likely driven by end-of-week demand peaks.
- **Night shifts on Wednesday and Monday** showed the most consistent high returns, suggesting evening weekday shifts as the most reliable strategy.
- **Thursday** showed consistently low values across all periods, confirming that the issue is structural to the day rather than limited to a specific time window.
- Analyzed average fuel cost per day of the week using daily aggregation to avoid duplication.
- Compared number of trips, average distance, and average rentability per day to understand volume vs quality dynamics.

### 4. Trip Volume vs Quality Analysis
- Compared number of trips per day of the week to identify demand patterns.
- Cross-referenced trip volume with average distance and rentability to evaluate whether busier days translate into higher earnings.
- **Thursday** has 212 trips (2nd highest) but the lowest average distance (6.39km) and rentability (4.63€), proving that volume alone does not guarantee revenue.
- **Monday** has the fewest trips (161) but the highest average distance (8.67km) and rentability (5.70€), confirming that trip quality matters more than quantity.

### 5. Correlation Analysis
- Built a correlation heatmap between `Distância da viagem`, `Duracao_Minutos`, `Rendimento`, `Euro_Km`, and `Gorjeta`.
- Identified a strong positive correlation (0.94) between trip distance and revenue, confirming that longer trips are significantly more profitable.

---

## 📈 Visualizations

### Rentability by Day and Period
![](graphs/Days_with_the_best_rentability.png)

### Rentability by Day and Period (Detailed)
![](graphs/Rentability_by_Period_of_the_Day_by_Euro.png)

### Correlation Heatmap
![](graphs/Heatmap.png)

### Rentability by Location
![](graphs/Rentability_by_KM.png)

### Number of Trips vs Rentability by Day
![](graphs/Number_of_trips_by_day.png)

| Week_Day | distance_mean | rentability_mean |
|---|---|---|
| Monday | 8.67 | 5.70 |
| Tuesday | 7.67 | 5.46 |
| Wednesday | 7.65 | 5.40 |
| Thursday | 6.39 | 4.63 |
| Friday | 7.18 | 5.13 |
| Saturday | 6.31 | 4.55 |
| Sunday | 6.72 | 4.88 |

---

## 💡 Business Insights

### 📅 Rentability by Day and Period
- **Friday Afternoon** is the most profitable combination with an average of **5.46€**, followed by **Wednesday Night** at **5.21€**.
- **Thursday** is the weakest day — no period exceeds an average of **4.00€**, making it consistently the worst performing day of the week.
- **Monday** stands out for having the best overall average across periods.

### ⛽ Fuel Cost
- The days with the highest fuel spend are **Monday, Tuesday, and Wednesday**, which aligns with them being the most active and profitable shifts.
- **Sunday and Saturday** have the lowest fuel cost, but this is expected as the car is driven significantly less on weekends.

### 🚗 Trip Volume
- The days with the most trips are **Friday and Thursday** — however, as shown in the analysis, volume alone does not translate into higher earnings.

### 📍 Rentability by Location
- **Espinho and Ermesinde** show the highest average €/km, making them the most profitable pickup origins.
- **Maia and Matosinhos** rank last in €/km rentability.
- In terms of time efficiency, **Vila Nova de Gaia and Avintes** are the fastest areas. On the other hand, **Maia and Ermesinde** are the least time-efficient.

---

## 🔍 Conclusions

- **Thursday is the biggest finding.** No period on Thursday exceeds 4.00€ average, yet it is the 2nd busiest day with 212 trips. The data shows the trips are simply shorter and less valuable. If I were to work for a TVDE company again, Thursday would be my day off — not the weekend.

- **Fuel cost savings on Thursday:** The average weekly fuel cost across the 5 working days is **18.96€**. Replacing Thursday with a day off would represent approximately **16% fuel savings**. Instead, those Thursday periods could be redistributed to underexplored slots in other days — for example, **Sunday Evening** shows surprisingly competitive numbers compared to other days.

- **More data is needed**, particularly for weekends. Sunday Morning has no data at all, which limits conclusions for that period.

- **Trips starting and ending in Vila Nova de Gaia are consistently good trips** — efficient, fast, and well compensated.

- **The airport (Maia) is a counterintuitive case.** Despite offering longer trips, it has the lowest €/km rentability. Longer does not mean more profitable — other locations consistently outperform Maia in revenue per kilometer. Most Maia trips originate from or go to the airport, which skews the entire location's performance downward.



