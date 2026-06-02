# TÜİK Forecasting Project

## 1. Project Overview

This project forecasts the annual number of museum and archaeological site visitors in Türkiye using official data from the Turkish Statistical Institute (TÜİK). The purpose of the project is to access a TÜİK time series directly through R, apply alternative forecasting methods, compare their forecasting performance, and select the most suitable method for forecasting the next available period.

## 2. Data Source and TÜİK Connection

The data were accessed directly from the TÜİK Data Portal using the `tuikr` R package.

* TÜİK data set name: Museum and Archaeological Site Visitor Statistics
* TÜİK theme/category: Culture and Sports
* TÜİK table name: Number of Visitors to the Museums and Ruins
* TÜİK dataflow ID: TR,DF_MUZE_ORENYER_ZYARETCI,1.0
* Selected variable: Museum and archaeological site visitor count
* Geographic coverage: Türkiye
* Data frequency: Annual
* Time coverage: 2001–2024
* Latest available observation: 2024
* Forecast target period: 2025
* Date of data access: 2026-06-03
* R package used for data access: `tuikr`
* Package source: https://github.com/emraher/tuikr

The selected TÜİK table was identified in R using the `tuikr` package. The data were then accessed reproducibly within the R Markdown notebook. No manually downloaded, manually edited, or separately created data file was used.

## 3. Research Objective

The objective of this project is to forecast the annual number of museum and archaeological site visitors in Türkiye for 2025.

This variable is meaningful for forecasting because museum and archaeological site visitor numbers reflect cultural participation, tourism activity, and public interest in cultural heritage. The series also contains a visible long-term trend and a major structural change during the COVID-19 period, making it suitable for comparing different forecasting methods.

## 4. Use of TÜİK Data in R

The TÜİK data were accessed and processed only within R. After importing the data, the following steps were performed:

* the relevant TÜİK table was identified,
* the selected variable was filtered,
* Türkiye-level total observations were selected,
* the annual frequency was confirmed,
* observations were arranged chronologically,
* missing values were checked,
* the data were transformed into a time series structure for forecasting.

The selected variable was the annual museum and archaeological site visitor count for Türkiye. The latest available observation was 2024, so the next forecast target period was 2025.

## 5. Exploratory Time Series Analysis

The time series covers annual observations from 2001 to 2024. The series generally shows an upward long-term trend. Visitor numbers increased strongly over the sample period, although there was a sharp decline in 2020 due to the COVID-19 pandemic.

After 2020, the series recovered rapidly and reached its highest observed value in 2024. Since the data are annual, no recurring seasonal pattern is present. The extracted series did not contain missing visitor values.

## 6. Forecasting Methods Applied

The following forecasting methods were considered:

* Naïve Forecasting: applied
* Moving Average: applied using a three-year window
* Weighted Moving Average: applied using weights of 0.2, 0.3, and 0.5
* Exponential Smoothing: applied with alpha = 0.30
* Trend-Adjusted Exponential Smoothing: applied because the series contains a visible trend
* Linear Trend Projection: applied using a time trend regression
* Seasonal Indices: not applicable because the data are annual
* Additive Decomposition: not applicable because the annual series has no seasonal component
* Multiplicative Decomposition: not applicable because the annual series has no recurring seasonality
* Regression with Trend and Seasonal Dummy Variables: not applicable because annual data do not contain seasonal periods

Seasonal methods were not omitted silently. They were evaluated as not applicable because the selected TÜİK time series has annual frequency.

## 7. Forecast Accuracy Comparison

The forecasting methods were compared using the following measures:

* Bias / Mean Error
* MAD
* MSE
* MAPE
* RSFE
* Tracking Signal

The comparison table is saved in:

`outputs/tables/accuracy_comparison.csv`

Among the applicable methods, Linear Trend Projection produced the lowest MAPE value. The main results were:

* Linear Trend Projection: MAPE = 26.09%
* Trend-Adjusted Exponential Smoothing: MAPE = 28.00%
* Naïve Forecasting: MAPE = 28.25%
* Exponential Smoothing: MAPE = 29.37%
* Weighted Moving Average: MAPE = 30.12%
* Moving Average: MAPE = 32.18%

## 8. Selection of the Superior Method

Linear Trend Projection was selected as the superior forecasting method.

This method was selected because it had the lowest MAPE and MSE among the applicable methods. It is also suitable for the structure of the selected time series because the annual visitor count shows a clear long-term upward trend and does not contain seasonality.

The estimated trend equation was:

Visitors = 13,319,946 + 1,595,677 × Time

The positive slope indicates that the annual number of visitors increased by approximately 1.6 million visitors per year on average.

## 9. Final Next-Period Forecast

The final forecast was produced using Linear Trend Projection.

* Selected superior method: Linear Trend Projection
* Date of data access: 2026-06-03
* Latest available TÜİK observation: 2024
* Forecast target period: 2025
* Forecasted value: 50,020,512 visitors

The final forecast result is saved in:

`outputs/tables/final_forecast.csv`

## 10. Interpretation of Results

The forecast suggests that the number of museum and archaeological site visitors in Türkiye is expected to be approximately 50.0 million in 2025.

Although the actual value in 2024 was higher than the forecasted 2025 value, the selected model estimates the long-term average trend rather than only following the most recent observation. The COVID-19 shock and the rapid post-pandemic recovery created large fluctuations in the series, which should be considered when interpreting the forecast.

## 11. Limitations

Several limitations should be considered:

* The data are annual, so the number of observations is limited.
* The series contains a major structural break in 2020 due to the COVID-19 pandemic.
* The analysis uses only historical visitor counts.
* Economic conditions, tourism policies, exchange rates, transportation conditions, and international travel trends were not included as explanatory variables.
* Seasonal forecasting methods could not be applied because the data are annual.

## 12. Reproducibility

To reproduce the project, open the repository and run the R Markdown file:

`forecasting_project.Rmd`

The notebook accesses the TÜİK data directly in R, prepares the time series, applies the forecasting methods, calculates accuracy measures, creates output tables, and saves the plots automatically.

The rendered HTML output is provided as:

`forecasting_project.html`

## 13. Repository Structure

The repository contains the following files and folders:

* `README.md`: project documentation
* `forecasting_project.Rmd`: main R Markdown notebook
* `forecasting_project.html`: rendered notebook output
* `outputs/tables/accuracy_comparison.csv`: model accuracy comparison table
* `outputs/tables/final_forecast.csv`: final forecast result
* `outputs/figures/`: actual vs forecast plots
* `R/data_import.R`: data access script
* `R/forecasting_methods.R`: forecasting method script
* `R/accuracy_measures.R`: accuracy calculation script
* `R/plots.R`: plot generation script
* `.gitignore`: ignored local files

## 14. Author

* Student Name: Sabiha Gülçin Özkan
* Course: Quantitative Analysis and Desicion Making
