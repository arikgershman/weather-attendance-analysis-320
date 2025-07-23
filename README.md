# Weather and College Class Attendance Analysis 🌦️

This project investigates the correlation between weather conditions and class attendance for two sections of the Spring 2025 CMSC320: Introduction to Data Science course at the University of Maryland. The goal was to determine if weather patterns significantly impact student presence in class, providing insights that could potentially help professors adjust their lecture plans.

## Project Overview

The project involved integrating attendance data with historical weather data, performing time-series decomposition, and performing statistical analysis to identify potential correlations and relationships.

## Files Included

* **`weather_attendance.ipynb`**: A Jupyter Notebook (Google Colab format) containing all the Python code for data loading, preprocessing, time-series decomposition, correlation analysis, and visualization. This notebook provides a detailed, executable walkthrough of the entire analysis.
* **`weather_attendance.pdf`**: A PDF presentation summarizing the project's objectives, data sources, methodology, results, and conclusions. This is ideal for a quick overview of the project.

## Data Sources

1.  **Attendance Data**: Provided as CSV files (`counts.csv`). This data was originally derived from classroom images of two sections (one large, one small) of the CMSC320 course in Spring 2025.
    * *Note: The attendance counts were obtained from a peer's computer vision analysis, which was posted on the class forum. My role in this project focused on the data analysis and correlation, not the computer vision aspect.*
2.  **Weather Data**: Provided as a CSV file (`hw5_weather.csv`). This dataset includes daily weather metrics such as:
    * `max_temp` (Maximum Temperature)
    * `min_temp` (Minimum Temperature)
    * `avg_temp` (Average Temperature)
    * `temp_departure` (Temperature Departure from Normal)
    * `HDD` (Heating Degree Days)
    * `CDD` (Cooling Degree Days)
    * `precipitation` (Precipitation in inches)
    * `new_snow` (New Snowfall in inches)

## Methodology

1.  **Data Loading and Merging**:
    * Attendance and weather data were loaded into Pandas DataFrames.
    * The datasets were merged based on the date.
    * Missing or 'T' (trace) values in `precipitation` and `new_snow` were converted to numerical (float) values.

2.  **Data Separation**:
    * Attendance data was separated into two distinct series: Monday/Wednesday (M/W) for the smaller section and Tuesday/Thursday (T/TH) for the bigger section, as their attendance patterns might differ.

3.  **Time-Series Decomposition (STL)**:
    * STL (Seasonal-Trend decomposition using Loess) was applied to both M/W and T/TH attendance series. This technique decomposes a time series into three components:
        * **Trend Component**: The long-term progression of the series.
        * **Seasonal Component**: The repeating pattern over a fixed period (e.g., weekly).
        * **Residual Component**: The remaining irregular fluctuations after removing trend and seasonality.
    * The **residual components** (detrended and deseasonalized attendance) were used for correlation analysis to focus on the unpredictable fluctuations in attendance.

4.  **Correlation Analysis**:
    * **Pearson Correlation**: Calculated to measure the linear relationship between the attendance residuals and each weather feature.
    * **Spearman Correlation**: Calculated to measure monotonic relationships (linear or non-linear) between the attendance residuals and each weather feature.
    * **P-value**: Computed for Spearman correlation to assess the statistical significance of the observed relationships (probability of seeing the relationship by chance). A significance level ($\alpha$) of $0.05$ was used.

## Results & Conclusion

The analysis found **no statistically significant correlation** between class attendance (after detrending and deseasonalizing) and any of the investigated weather features at an alpha level of $0.05$.

**Notable (but not statistically significant) trends observed:**

* **Monday/Wednesday Section**:
    * A positive correlation with precipitation (Pearson $\approx 0.562$, Spearman $\approx 0.516$, p-value $\approx 0.059$). This was close to significance, suggesting a slight tendency for attendance to increase with more precipitation, which is counter-intuitive.
* **Tuesday/Thursday Section**:
    * A negative correlation with new snow (Pearson $\approx -0.500$, Spearman $\approx -0.397$, p-value $\approx 0.102$). This suggests a tendency for attendance to decrease with more new snow, which aligns with intuition but was not statistically significant.
    * A positive correlation with maximum temperature (Pearson $\approx 0.255$, Spearman $\approx 0.116$, p-value $\approx 0.647$).
    * A negative correlation with precipitation (Pearson $\approx -0.350$, Spearman $\approx -0.188$, p-value $\approx 0.455$).

**Overall Conclusion:**
Based on this analysis, professors **should not rely on weather conditions to significantly impact class attendance** when preparing lectures for this specific course and timeframe.

**Future Work:**

* **Collect More Data**: A larger dataset over multiple semesters could reveal more statistically significant trends.
* **Analyze Other Variables**: Explore other potential factors influencing attendance (e.g., exam schedules, assignment deadlines, time of day, course difficulty, instructor popularity).
* **Redesign Class Structure/Teaching Style**: If attendance remains a concern, consider teaching modifications independent of weather.

## Technologies Used

* **Python**
* **Pandas**: For data manipulation and cleaning.
* **Matplotlib**: For data visualization.
* **Statsmodels**: For time-series decomposition (STL).
* **NumPy**: For numerical operations, including correlation calculations.
* **SciPy (stats)**: For Spearman correlation and p-value calculation.
* **Google Colab**: For interactive analysis and documentation.
