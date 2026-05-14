# TVDE-Uber-Analysis
Exploratory performance and profitability analysis of my TVDE fleet using Python, Pandas, and Matplotlib/Seaborn. I decided to use python, because it was the most difficult class for me in my course

## 📌 Project Overview

This project involves a strategic analysis of real TVDE trip data collected over three months. We used Python for data processing and visualisation, and our main goal was to identify patterns in rentability, trip efficiency and fuel cost impact across different days of the week, periods of the day and pickup locations. This provides a data-driven perspective on how to maximise net profit per trip and to understand what I did wrong when administering.

## 🛠️ Tech Stack

*Python / Pandas: Used for data cleaning, transformation, merging datasets, and feature engineering.
*Matplotlib / Seaborn: Applied for data visualization and pattern discovery.
*Excel: Source format for raw trip data and fuel cost records.
*Jupyter Notebook: Used as the development and reporting environment.

## 📁 Project Structure
- `Limpeza de dados.ipynb` — data cleaning and preparation
- `CP_Grande_Porto.ipynb` — postal code processing
- `Gráficos.ipynb` — visualizations and analysis

1. Data Preparation & Cleaning

*Merge multiple monthly Excel files into a single data frame using Power Query.
  *'Limpeza de dados.ipynb' – where the data was cleaned, processed and prepared for analysis.
* Extracted temporal features, such as Period_of_Day (Morning, Rush Hour, Afternoon, Evening or Night) and Week_Day, from the trip timestamp.
Handled missing postal codes by mapping them to locality names and filling in unmatched values as 'Others'.
  *CP_Grande_Porto.ipynb handles raw data with the postal codes of Portugal. I cleaned the data and extracted only the Porto postal codes, which I used to create the nome_localidade_destino and nome_localidade_origem columns. The main file contained too much sensitive information, so I decided to use only the postcode.
* Calculated Rendimento (revenue per trip) and Lucro_Liquido (profit per trip), the latter being Rendimento - Custo_Combustivel.
  * Imported a separate fuel transaction dataset and calculated the average fuel cost per km (Custo_Combustivel).
* Calculated 'Euro_Km' (revenue per km) as a rentability metric per trip.

2. Correlation Analysis

 *Built a correlation heatmap between Distância da viagem, Duracao_Minutos, Rendimento, Euro_Km, and Gorjeta.
 *The objective of the heatmap was to identify the columns with the strongest correlation.

3. Rentability by Location

  *Filtered locations with more than 10 trips to ensure statistical relevance.
  *Ranked pickup locations by average Euro_Km to identify the most and least profitable origins.
  *Cross-referenced with average trip duration to identify locations that are both fast and profitable.

4. Temporal Pattern Analysis

  *Built a pivot table using Week_Day vs Period_of_Day with mean Lucro_Liquido to identify the best combinations of day and time.
  *Friday Afternoon emerged as the top outlier (5.46€), likely driven by end-of-week demand peaks.
  *Night shifts on Wednesday and Monday showed the most consistent high returns, suggesting evening weekday shifts as the most reliable strategy.
  *Analyzed average fuel cost per day of the week using daily aggregation to avoid duplication.
  *Compared number of trips, average distance, and average rentability per day to understand volume vs quality dynamics.

5.Trip Volume vs Quality Analysis

  *Compared number of trips per day of the week to identify demand patterns.
  *Cross-referenced trip volume with average distance and rentability to evaluate whether busier days translate into higher earnings.
  *Thursday has 212 trips (2nd highest) but the lowest average distance (6.39km) and rentability (4.63€), proving that volume alone does not guarantee revenue.
  *Monday has the fewest trips (161) but the highest average distance (8.67km) and rentability (5.70€), confirming that trip quality matters more than quantity

📈 Visualizations
## Correlation Heatmap
<img width="640" height="480" alt="Heatmap" src="https://github.com/user-attachments/assets/b76d342a-784d-4d50-b69d-854bf0c069ca" />

## Rentability by Location
<img width="513" height="465" alt="image" src="https://github.com/user-attachments/assets/71b05b32-b891-415a-89bf-b8f25961c45c" />

## Temporal Pattern Analysis
<img width="1200" height="800" alt="Days with the best rentability" src="https://github.com/user-attachments/assets/3589a356-f6cd-44d4-b6b6-e875902d91a7" />

## Trip Volume vs Quality Analysis
<img width="640" height="480" alt="Number of Trips by day" src="https://github.com/user-attachments/assets/dcce83a7-5961-490f-90c6-1349c591a32d" />
<img width="278" height="262" alt="image" src="https://github.com/user-attachments/assets/57e39ed4-702d-4ca4-9d15-d216dc33e728" />

💡 Business Insights

*Monday and Wednesday nights are the most profitable combinations (5.05€ and 5.21€ net per trip), making them the priority shifts to maximize earnings.

*Friday Afternoon is the single best combination (5.46€), likely driven by end-of-week demand peaks. However, Wednesday and Monday nights offer the most consistent high returns, making evening weekday shifts the most reliable strategy overall.

*Espinho and Matosinhos are the most rentable pickup origins (1.06€ and 1.03€/km), while Maia is the worst (0.52€/km) — long trips but poorly compensated.

*Afternoon and Rush hour consistently yield the highest Euro/Km (0.82€ and 0.80€), making them the most efficient periods to work.

*Thursday is a paradox — the 2nd busiest day with 212 trips, yet the lowest rentability (4.63€ avg) and shortest average distance (6.39km). High volume does not equal high revenue; trip quality matters more than trip quantity.

*Sunday mornings show zero activity, and the weekend in general underperforms compared to weekdays in both rentability and trip distance.

*After accounting for fuel costs, the net profit picture shifts significantly, reinforcing the importance of prioritizing longer, higher-value trips over maximizing trip count.
