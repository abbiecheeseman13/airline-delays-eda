# airline-delays-eda
Airline Delays Exploratory Data Analysis

This project explores and models airline delay data using Exploratory Data Analysis (EDA), data preprocessing, and a linear regression model.  
The goal is to predict **average arrival delay minutes per flight** based on features such as carrier, airport, year, month, and flight counts.

---

## 📊 Dataset

The dataset comes from the Bureau of Transportation Statistics (BTS) airline delay cause reports.  
It includes fields such as:

- `carrier` – airline code  
- `carrier_name` – airline full name  
- `airport` – airport code  
- `airport_name` – airport full name  
- `year`, `month` – reporting period  
- `arr_delay` – total arrival delay minutes (target source)  
- `arr_flights` – number of arriving flights  
- `carrier_delay`, `weather_delay`, `nas_delay`, `security_delay`, `late_aircraft_delay` – component delay minutes  
- `arr_del15`, `arr_cancelled`, `arr_diverted` – flight counts by status  

Since `arr_delay` represents **total minutes** (heavily dependent on the number of flights), we instead model:

delay_per_flight = arr_delay / arr_flights

This gives a more meaningful outcome: **minutes of delay per flight**.

---

## 🛠 Methods

1. **Exploratory Data Analysis (EDA)**
   - Data summary, missing values, duplicates
   - Distribution of delays
   - Average delays by carrier
   - Correlation heatmaps for numeric features

2. **Preprocessing**
   - Handling missing values (`SimpleImputer`)
   - Standardization for numeric features (`StandardScaler`)
   - One-hot encoding for categorical features (`OneHotEncoder`)
   - Dropping leakage columns like component delays (to avoid directly encoding the target)

3. **Modeling**
   - Linear Regression (`sklearn.linear_model.LinearRegression`)
   - Target variable: `delay_per_flight` (minutes/flight)
   - Evaluation metrics: RMSE, MAE, R²

4. **Prediction Helpers**
   - Functions to build a baseline feature template (median/mode values)
   - Override selected features (e.g., carrier, airport, year, month) to test scenarios
   - Predict per-flight delay and scale to total delay given `arr_flights`
  
