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
- stats

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

## Time Series Exploratory analysis
ETS decomposition was done on the various time series variables to detect trends, seasonality and residual. 
A correlation matrix for the numerical features was computed to check for multicollinearity.  

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
   

