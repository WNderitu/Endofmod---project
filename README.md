# **30 Day Forecast: Amberpet Mandal Weather Conditions**

## Introduction

**Telangana**
- Telangana is one of the states in India, situated in the south-central part of the Indian subcontinent on the high Deccan Plateau.
- The capital city of Telangana State is Hyderabad.
- Telangana state is divided into 33 districts which are further divided into 584 mandals.
- Hyderabad district is divided into 16 mandals. 
- Amberpet is a mandal in Hyderabad District.
  
**Climate**
- Telangana is a semi-arid area and has a predominantly hot and dry climate. 
- Summers start in March, and peak in mid-April with average high temperatures in the 37 –38 °C (99 - 100 °F) range. 
- The monsoon arrives in June and lasts until Late-September with about 755 mm (29.7 inches) of precipitation. 
- A dry, mild winter starts in late November and lasts until early February with little humidity and average temperatures in the 22 - 23 °C (72–73 °F) range.
- The daily weather conditions for Telangana State are available from February 1, 2023, to January 31, 2025.
- The data has been extracted from Open Data Telangana. With this data, the weather conditions for the next 30 days can be predicted from the available data. 

## Problem Statement
Weather forecasting is important for public safety, agriculture, transportation, and daily life, as it allows people to prepare for weather events and make informed decisions. 
It helps save lives by predicting severe weather, supports farmers in planting and harvesting, guides travel planning, and enables businesses to manage energy use. 

## Project Objectives
- To develop a multivariate time series forecast model for predicting the daily weather conditions for the next 30 days for Amberpet Mandal. 
- To forecast the following daily weather conditions for the next 30 days for Amberpet Mandal using the developed model;
- Rain (mm)
- Min Temp (°C)
- Max Temp (°C)
- Min Humidity (%)
- Max Humidity (%)
- Min Wind Speed (Kmph)
- Max Wind Speed (Kmph) 

## Methods Used
- Descriptive statistics
- Bivariate and multivariate statistics
- Data visualization
- Machine learning - Multivariate Time Series Forecasting - VAR Model

## Technologies
- Python
- Pandas
- Seaborn
- Matplotlib
- Jupyter
- Scikit learn
- statsmodel

## Project Description
The project will entail conduct of the following:
- Importation of the datasets
- Conduct of exploratory data analysis using different statistical techniques and visualization of the data
- Conduct data pre-processing & feature engineering
- Development and evaluation of a Multivariate Time Series Forecasting - VAR Model
- Forecast using VAR Model
- Determination of the next steps. 

## Dataset
The Telangana weather dataset is derived from Hugging Face website - https://huggingface.co/datasets/ron-the-code/Telangana_time_series_2023-2025

Consist of 7 numerical target variables containing data on:
 - Rain (mm)
 - Min Temp (°C)
 - Max Temp (°C)
 - Min Humidity (%)
 - Max Humidity (%)
 - Min Wind Speed (Kmph)
 - Max Wind Speed (Kmph)
   
Additional data variables are date, district and mandal.

The datasets used are saved in this repository. 

## Exploratory Data Analysis
The data was analysed using pandas. Descriptive statistics was used to summarise the numerical variables. Seaborn and matplotlib were used for data visualization. Line plots were used to show the trend of the different weather conditions over time. Histogram and Box plots were used to describe data distribution, data spread and detect outliers.

Distribution of weather variables

Histograms

<img width="1491" height="1025" alt="image" src="https://github.com/user-attachments/assets/02661fe4-f834-4e8f-b291-ab409270d038" />

**1. Rain (mm) - Extreme Right Skew**
- Massive spike at 0 (most days are dry)
- Long right tail with rare heavy rainfall events
- NOT normally distributed despite the overlay curve

**2. Temperatures - Approximately Normal distribution**
- Min Temp: Slight left skew, but reasonable
- Max Temp: Nearly perfect normal distribution

**3.Humidity Variables - Different Behaviors**
- Min Humidity: Roughly normal distribution with slight right skew
- Max Humidity: Left-skewed (clustered near 100%). Many days hit 100% max humidity (morning dew/fog)

**4.Min Wind Speed - Zero-Inflated models recommended**
- Extreme concentration at 0 km/h. Essentially useless for prediction

**5.Max Wind Speed - Right Skewed**
- Most days have low wind (5-15 km/h). Rare extreme wind events (outliers up to 70 km/h)

Box plots

<img width="1490" height="989" alt="image" src="https://github.com/user-attachments/assets/c2777fe9-8890-49af-a5e1-2d0ce611d1eb" />

- Rain (mm) - right-skewed, many outliers—typical of sporadic heavy rainfall.
- Min Temp (°C)	Narrow IQR (21 - 25 degrees), a few outliers either low temps or high temps, suggesting stable nighttime temperatures.
- Max Temp (°C)	Wider spread (31 - 36 degrees), possibly seasonal variation or daytime extremes, many outlier temps either low or high temps
- Min Humidity (%) - many outliers in the higher % range, wide spread
- Max Humidity (%) - Possibly left-skewed—high humidity is common, but extreme lows are rare, some outliers. wide spread
- Min Wind Speed (Kmph) - tight distribution, possibly near-zero values, many outliers. 
- Max Wind Speed (Kmph) - Wider range, many outliers during storms or gusts.(higher speeds). Overall lower peak wind speeds. 

Box plots by month to visualize seasonal variations and outliers

<img width="1390" height="1589" alt="image" src="https://github.com/user-attachments/assets/b448b793-d72b-44ad-9538-ad336c375600" />

**Weather Pattern Insights**

**1. Rain (mm) - Highly Seasonal & Sparse**
- Monsoon months (Jun-Sep): Heavy rainfall with many outliers. Dry months (Oct-May): Mostly 0 mm (boxes are flat)

**2. Temperature - Clear Seasonal Cycles**
- Hottest: April-May (pre-monsoon summer). Coolest: December-January (winter). Min Temp range: 14-30°C, Max Temp: 24-43°C
- **Strong seasonal pattern 

**3. Humidity - Monsoon Effect**
- Max Humidity: Consistently high (80-100%) across months. 
- Min Humidity: Drops significantly in dry months. Jan-May: 20-40%. Jul-Aug: High min humidity due to monsoon.
- **Clear inverse relationship with temperature**

**4. Wind Speed Issues**
- **Min Wind Speed:**
  - Nearly all months show 0 km/h median with extreme outliers, all months.
 - **Max Wind Speed:**
  - July spike is dramatic (15-47 km/h median, up to 70 km/h). 
  - Monsoon wind storms clearly visible. 
  - **Many outliers - alot in August. Other months - June, September, November, December**

Correlation Analysis

<img width="711" height="590" alt="image" src="https://github.com/user-attachments/assets/2e24915e-2cb9-4375-95cf-51d62fad52ae" />

**Strong correlations**
- **Max Humidity vs. Min Humidity (0.69)** - strong positive correlation. Days with high peak humidity also tend to have higher minimum humidity. Suggests consistent moisture levels across the day—possibly during monsoon or humid seasons.
- **Max Temp vs. Min Humidity (-0.66)** - strong negative correlation. As daytime temperatures rise, the minimum humidity tends to drop. This reflects typical diurnal drying—hotter air holds more moisture, lowering relative humidity unless moisture increases
- **Max Humidity vs. Max Temperature (-0.52)** - moderate negative correlation: As peak humidity increases, peak temperatures reduce. 
  
**Weak correlations**
- Min Temp vs. Rain (-0.04) - weak negative correlation
- Min Humidity vs. min Temp (0.06) - weak positive correlation
## Time Series Exploratory analysis
ETS decomposition was done on the various time series variables to detect trends, seasonality and residual. 
A correlation matrix for the numerical features was computed to check for multicollinearity.  

Line Plots

<img width="1487" height="590" alt="image" src="https://github.com/user-attachments/assets/c161ca6e-ac22-44e6-8f82-94a8a806025d" />

**Daily Rainfall Trends - Amberpet Mandal (Jan 2023– Feb 2025)**

Seasonal Rainfall Patterns:
- Monsoon Peaks - significant spikes in rainfall occur during the monsoon months (June to September) in both 2023 and 2024.These peaks are consistent with the monsoon season in Telangana, which typically brings heavy rainfall.
- Dry Periods - minimal or no rainfall is observed during the dry months (October to May), reflecting the semi-arid climate of the region.
Rainfall Intensity:
- Heavy Rainfall Events - some days experience rainfall exceeding 70 mm, indicating intense rainstorms during the monsoon.
- Low Rainfall Days - most days have little to no rainfall, as shown by the flat sections of the graph.
Yearly Trends:
- The rainfall pattern is consistent across 2023 and 2024, with similar monsoon peaks and dry periods.
- This highlights the predictable nature of rainfall in Amberpet Mandal, driven by the region's climate.

<img width="1487" height="590" alt="image" src="https://github.com/user-attachments/assets/8d794146-1fb0-4bfb-8587-fd947d45aa40" />

**Temperature Trends – Amberpet Mandal (Jan 2023– Feb 2025)**
- The chart illustrates the daily minimum and maximum temperature trends in Amberpet Mandal from January 2023 to Feb 2025.
- The data shows **clear seasonal patterns,** with temperatures peaking between April and June each year (maximums often above 40°C) and reaching their lowest between December and January (minimums around 15–18°C). 
- The **gap between daily highs and lows widens during summer months**, indicating hot days and warm nights, while **winter months show smaller differences**, reflecting cooler days and cold nights. 
- Overall, the **temperature pattern remains consistent over the two-year period,** highlighting the region’s tropical climate characterized by hot summers, mild monsoons, and cool winters.

<img width="1487" height="590" alt="image" src="https://github.com/user-attachments/assets/f777da93-7b3c-4f5d-84eb-8eb28583368a" />

**Humidity Trends - Amberpet Mandal (Jan 2023– Feb 2025)**
- The analysis of minimum and maximum humidity levels from January 2023 to February 2025 shows a clear seasonal humidity cycle typical of a monsoon-influenced climate. 
- Maximum humidity consistently remains high (70–100%) throughout the year, peaking during the monsoon months (June–October), when the air is nearly saturated with moisture. 
- Minimum humidity values display strong variation, dropping as low as 10–20% during the pre-monsoon dry season (March–May), reflecting hot and arid daytime conditions.
- The large gap between minimum and maximum humidity outside the monsoon period indicates significant diurnal variation, driven by daytime heating and nighttime cooling. Conversely, this gap narrows during the monsoon, showing persistently moist air
- Overall, these trends highlight a predictable humidity pattern - **strong annual humidity cycle**

<img width="1487" height="590" alt="image" src="https://github.com/user-attachments/assets/d52ccf60-4b2a-4620-aeb8-2a8282e6304a" />

**Wind Speed Trends - Amberpet Mandal (Jan 2023– Feb 2025)**
Seasonal Variation
- Recurring seasonal pattern in wind speeds, with peaks occuring mainly during mid-year months (June–August) — consistent with monsoon or pre-monsoon activity.
- Lower speeds dominate in winter months (Dec–Feb), indicating calmer atmospheric conditions.

Wind Speed Peaks
- Notable spikes occur around:
  - April–August 2023: Max wind speeds reach nearly 70 km/h.
  - June–August 2024: Another intense period, again reaching around 65–70 km/h.
- These spikes correspond to strong monsoon winds

Min Wind Speed Trends
- The minimum wind speeds stay close to 0–5 km/h most of the time.
- Slight rises in min speeds during May–August months show that even base wind activity increases during monsoon periods.
  
Post-Peak Calm
- After September 2024, both min and max speeds drop and stabilize, showing the end of windy or stormy conditions.

ETS Decomposition Plots

<img width="613" height="356" alt="image" src="https://github.com/user-attachments/assets/e95a9848-62d8-46fe-96ae-1c972d395ae3" />

- **Trend** - slight dip in rainfall levels during late 2023 & early 2024, followed by stabilization - changes in overall rainfall patterns over the 2-year period that could be a temporary shift
- **Seasonal** - strong seasonal component present – highlights predictable nature of rainfall cycles, account for monsoon seasonality
- **Residual** - small & scattered, indicating most of variability in rainfall is explained by the trend & seasonal components

<img width="463" height="268" alt="image" src="https://github.com/user-attachments/assets/c827d6af-3741-40de-987f-326162e388e8" />

<img width="477" height="277" alt="image" src="https://github.com/user-attachments/assets/07c7e65d-391e-48c1-9f84-33e3678166ba" />

- **Trend**
  - gradual ↓ in min temps from mid-2023 to early 2025 - due to changes in weather patterns or other environmental factors. Declining trend in min temps can help predict long-term changes in the region's climate.
  - gradual ↑ in max temps from mid-2023 to early 2025, could indicate warming trends or seasonal shifts in region’s climate
- **Seasonal**
  - Repeating seasonal patterns. Peaks & troughs visible, reflecting higher min & max temps during summer months & lower min & max temps during winter months. Predictable nature of temp cycles. Strong seasonal component - account in model
- **Residual** - relatively small, indicating  most of variability in min & max temp is explained by the trend & seasonal components. 

<img width="447" height="258" alt="image" src="https://github.com/user-attachments/assets/3ba59753-f356-49c8-93e4-d3e174b0b47f" />

<img width="461" height="260" alt="image" src="https://github.com/user-attachments/assets/5caa9736-6f7a-4137-9eec-c6fbf347dcb5" />

- **Trend**
  - Initial ↑ in min humidity in mid-2023, followed by gradual decline from late 2023 to early 2025
  - Initial ↓ in max humidity in mid-2023, followed by a gradual incline from late 2023 to early 2025
  - Could indicate changes in weather patterns or environmental factors affecting humidity levels - help predict long-term changes in the region's climate.
- **Seasonal**
  - Repeating seasonal patterns in min & max humidity – highlights predictable nature of humidity cycles, account for seasonality in model
  - Peaks & troughs are visible – reflect higher min humidity & max humidity during monsoon months (June–September), lower min & max humidity during dry months (October–May)
- **Residual** - relatively small, indicating  most of variability is explained by the trend & seasonal components
  
<img width="444" height="259" alt="image" src="https://github.com/user-attachments/assets/56258adb-a655-4110-a584-1d6c815c1ddf" />

<img width="453" height="259" alt="image" src="https://github.com/user-attachments/assets/ff13b588-2190-42ef-911d-d2c5b12f1c85" />

- **Trend**
  - Initial ↑ in min wind speed from around July 2023 to the end of 2023, followed by gradual decline from late 2023 to around March 2024. Then the min weed speed doesn’t change much.
  - Max wind speed rises steadily from mid 2023, peaks until around March 2024, and then slightly declines. This is indicative of the monsoon season. 
- **Seasonal**
  - Repeating seasonal patterns in min & max wind speed. Peaks visible, reflecting higher min wind speeds during certain months (likely monsoon or pre-monsoon periods) & lower speeds during calmer months (summer & winter).
  - For max wind speed, pronounced peaks during the same periods as observed spikes, confirms strong seasonality—likely corresponding to monsoon season, hence predictable nature of wind speed cycles, account in models
- **Residual** - relatively small, indicating  most of variability is explained by trend & seasonal components. Max wind speed - most residuals are close to zero, but there are occasional outliers, indicating some extreme wind events not explained by regular patterns.

## Data Pre-processing and Feature engineering
Numerical columns with skewed data were log transformed with masking of zero values. 
Robust scaling was done for data with multiple outliers. 
Stationarity check was done using Augmented Dickey Fuller test. Three non-stationary variables were differenced.
ACF & PACF plots were visualised. 

## Insights
<img width="492" height="195" alt="image" src="https://github.com/user-attachments/assets/41f87b8b-6ed5-498a-bd91-a0a1310a1648" />

<img width="444" height="196" alt="image" src="https://github.com/user-attachments/assets/1aa21525-f2c8-49ac-89d1-0b7d92ce7561" />

<img width="444" height="196" alt="image" src="https://github.com/user-attachments/assets/f98437dd-2b59-4752-a2ed-171bb021d9e9" />

<img width="438" height="196" alt="image" src="https://github.com/user-attachments/assets/695b67f6-ce45-426e-9e32-f1ae5db3a662" />

<img width="430" height="196" alt="image" src="https://github.com/user-attachments/assets/5c89d032-9422-4332-9b05-21ad548e8106" />

<img width="429" height="196" alt="image" src="https://github.com/user-attachments/assets/375c3eb8-30ce-4e35-ae5c-aa5a633ee92a" />

<img width="438" height="195" alt="image" src="https://github.com/user-attachments/assets/48abc57a-f306-4141-93f5-764527dfaaee" />


<img width="902" height="414" alt="image" src="https://github.com/user-attachments/assets/3cec0973-b5ff-4d19-8a84-50c001c8cc11" />


## Machine learning Modelling
A Vector Autoregressor Model (VAR (4)) was used to forecast 30 day weather conditions for amberpet mandal. Evaluation metrics used were RMSE, MAE & MSE. 

## Recommendations/Next Steps
1. Determine how best to handle variables with outliers, skewed variables & many zero values
2. Create & incorporate a causality-informed feature mask into the VAR model
3. Validate model assumptions using residual diagnostics
4. Understand how shocks propagate by Impulse Response Analysis
5. Extend to VARMAX with exogenous regressors (e.g., seasonal indicators, Fourier terms)
6. Do univariate time series forecasting for each variable
7. Compare with deep learning models (e.g., XGBoost, LSTM) using same features

## Folder structure
The folder contains the following files:
1. 1_data cleaning notebook
2. 2_ eda notebook
3. 3_ featureengineering& forecast notebook
4. 30 Day Forecast: Amberpet Mandal Weather Conditions project presentation
5. Amberpet weather cleaned .csv - data used for EDA, feature enineering & model
6. Hyderabad_weather_data.csv - used for data cleaning
7. Telangana_combined_ weather_dataset - original dataset csv file
   
## Acknowledgements & Attributions
1. https://www.britannica.com/place/Telengana
2. Data Source - Hugging Face website - https://huggingface.co/datasets/ron-the-code/Telangana_time_series_2023-2025
   

