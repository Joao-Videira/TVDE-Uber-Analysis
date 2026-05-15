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

## 📈 Visualizations
## Correlation Heatmap
<img width="640" height="480" alt="Heatmap" src="https://github.com/user-attachments/assets/b76d342a-784d-4d50-b69d-854bf0c069ca" />

## Rentability by Location
<img width="513" height="465" alt="image" src="https://github.com/user-attachments/assets/71b05b32-b891-415a-89bf-b8f25961c45c" />

## Temporal Pattern Analysis
<img width="1200" height="800" alt="Days with the best rentability" src="https://github.com/user-attachments/assets/3589a356-f6cd-44d4-b6b6-e875902d91a7" />

## Trip Volume vs Quality Analysis
<img width="640" height="480" alt="Number of Trips by day" src="https://github.com/user-attachments/assets/dcce83a7-5961-490f-90c6-1349c591a32d" />
<img width="278" height="262" alt="image" src="https://github.com/user-attachments/assets/57e39ed4-702d-4ca4-9d15-d216dc33e728" />

## 💡 Business Insights

•    The most profitable periods are:
 o    Friday afternoon, with an average of €5.46, and Wednesday evening, with €5.21.
 o    It is worth noting that Thursday is the weakest day, with averages for all periods below €4.
 o    Monday also stands out for having the best average.

•    The days on which the most fuel is used, as we can see from the fuel cost chart, are: Monday, Tuesday and Wednesday.
•    The days on which the least fuel is used are: Sunday and Saturday, but we know these are the days when the car is driven the least.

•    In terms of journeys, the days with the most journeys are Friday and Thursday.

•    Looking at the profitability graph, we can see that Espinho and Ermesinde are the areas with the highest average min/km. Maia and Matosinhos are at the bottom.
•    In the time-based profitability graph, we can see that Vila Nova de Gaia is the most efficient, along with Avintes. On the other hand, Maia and Ermesinde are the least efficient.

## Conclusions
•     What immediately caught my eye was Thursday: there is no period when the average exceeds €4. Despite this, it is the second-busiest day in terms of journeys. Looking at the table, we can also see that the journeys are shorter. If I were to run the company again, my day off would most likely be Thursday rather than at the weekend.
•    The average weekly fuel consumption (here I’ve calculated using only the 5 working days because there are fewer journeys at the weekend) is €18.96, meaning that on Thursdays there was a fuel saving of around 16%. My recommendation is that Thursday needs to be reviewed, and we should try to replace those periods with other days when nobody is driving; for example, Sunday evening is quite interesting compared to the rest of the days.

•    I need more data, especially for the weekend; there is no data for Sunday morning, for example.

•    Journeys starting and ending in Vila Nova de Gaia are good journeys.

•    The airport is a case study; as we can see, it is where the most time is lost per journey and where there is also the lowest profitability per kilometre. In other words, it is counterintuitive: although the airport offers longer journeys, the company is losing money because other locations are more profitable. The airport is located in Maia, and most journeys from Maia are to the airport.



