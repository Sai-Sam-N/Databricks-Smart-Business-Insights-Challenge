# Databricks-Smart-Business-Insights-Challenge

#### Team Name : `OneDirection`

Team Members |
------------ |
Sai Samyuktha N |
Sri Lahari Chirumerla | 
Gyanadipta Mohanty |
Geyani Lingamallu |

Demo available on [YouTube](https://youtu.be/WyqRXaE4JNg?si=beZ8Pj4ZAurhc5lc)
<a href="https://youtu.be/WyqRXaE4JNg?si=beZ8Pj4ZAurhc5lc" target="_blank">
 <img src="http://img.youtube.com/vi/nTQUwghvy5Q/mqdefault.jpg" alt="Watch the video" width="240" height="180" border="10" />
</a>

---

### **ETA Prediction System: AI Dashboards, Genie Spaces, and Machine Learning Integration**

The Estimated Time of Arrival (ETA) Prediction System is an intelligent, end-to-end solution designed to forecast travel time between two locations based on real-time traffic and dynamic weather conditions. The system incorporates three integrated components: AI/BI Dashboards, Genie Spaces for data engineering, and a machine learning model built to deliver accurate, future-ready ETA predictions. The objective is to enhance urban commute planning and support data-driven mobility decisions.

---

### **Part 1: AI/BI Dashboards**

The project begins with the visualization of raw and processed data using interactive BI dashboards. These dashboards are not only a tool for exploratory data analysis but also serve as the decision-making interface for users and stakeholders. Built using tools compatible with real-time data feeds, the dashboards showcase:

* **Traffic trends** across hours, days, and weeks.
* **Historical vs. predicted ETA comparisons**, with insights into deviations.
* **Weather overlays** that help visualize how temperature, precipitation, humidity, and wind influence commute times.
* **Origin-destination route mapping**, showing frequently traveled routes and peak hour congestion.

The dashboards serve as a central reporting hub where the effectiveness of the ML model can be monitored, and new patterns can be discovered. Filters allow the user to select specific locations, dates, and weather conditions to simulate "what-if" scenarios for commute planning.

---

### **Part 2: Genie Spaces – Data Engineering Layer**

To support accurate model training and real-time prediction, the project leverages **Genie Spaces** for all data-related workflows. Genie Spaces is used for:

* **Data ingestion**: Collecting traffic data using Google’s Distance Matrix API and weather data using the Open-Meteo API.
* **Data enrichment**: Traffic data is augmented with hourly weather data by joining them on time and location.
* **Time-series alignment**: All records are resampled and interpolated to ensure a consistent hourly interval, with additional 30-minute points added by averaging surrounding values.
* **Data cleaning**: Missing values in critical weather features such as temperature, precipitation, and wind speed are imputed using smart rules and interpolation.
* **Feature engineering**: Time-based features (hour of day, day of week), location encoding (origin and destination), and combined windspeed features are computed to improve model input quality.

This layer ensures that all the inputs to the model are reliable, timely, and contextually aligned. Moreover, Genie automates the preprocessing pipeline so that future prediction queries can operate on freshly fetched data.

---

### **Part 3: Machine Learning Model**

The core of the system is a supervised machine learning model that predicts the **duration in traffic** (ETA) in minutes. The target variable is derived from the `duration_in_traffic_value` field, converted into minutes. The features used in training the model include:

* **Weather parameters**: Temperature (°C), relative humidity (%), precipitation (mm), and wind speed (km/h).
* **Temporal features**: Hour of the day and day of the week.
* **Location encodings**: One-hot encoded origin and destination values.
* **Distance and traffic metrics** (if available at prediction time).

A **RandomForestRegressor** was chosen for this task due to its ability to capture complex, non-linear relationships and robustness to outliers. The model was trained on historical traffic and weather data, covering multiple routes across Hyderabad.

---

### **Model Performance**

The model’s performance was evaluated using a holdout test set, and the following metrics were achieved:

* **Mean Absolute Error (MAE)**: 1.75 minutes
* **Root Mean Squared Error (RMSE)**: 3.07 minutes
* **R² Score**: 0.93

These metrics indicate that the model, on average, deviates by only 1.75 minutes from the actual ETA, with most predictions staying within 3 minutes of the true value. An R² score of 0.93 suggests the model explains 93% of the variance in the data — a strong indicator of predictive power.

---

### **Prediction for Future Time**

One of the unique features of the system is its ability to **forecast ETA for a future date and time**. This is made possible by:

1. **Dynamically fetching weather forecasts** from Open-Meteo API for the requested datetime and location.
2. **Combining it with time and location-based features**, ensuring the model receives inputs consistent with its training distribution.
3. **Using the trained RandomForest model** to return the predicted ETA in minutes.

This enables planning ahead — for example, predicting commute time for a 9 AM meeting tomorrow from Kondapur to Hitech City under forecasted rain.

---

### **Use Case and Impact**

This system is ideal for logistics firms, ride-hailing platforms, and city mobility planners who need to understand and optimize travel times under uncertain conditions. By blending historical trends, real-time weather, and predictive modeling, it offers an AI-powered assistant for urban travel.

It’s scalable, interpretable, and capable of being deployed as a REST API or embedded within mobile/web applications to support smarter transportation decisions.
---
