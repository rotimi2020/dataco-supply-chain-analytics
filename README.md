# DATACO Supply Chain Analytics

**Supply Chain Analytics | KNIME | Power BI | Machine Learning | Time-Series Forecasting**

## About the Project

How well is a supply chain performing? Where are delivery delays happening, which shipping methods perform better, and what can historical order data tell us about future demand?

This project explores these questions using the DataCo supply chain dataset. I used KNIME to prepare the data, perform business analysis, develop a late-delivery prediction workflow and forecast monthly order volumes. I then brought the results together in a five-page Power BI report.

The focus was not just on producing charts, but on turning operational data into information that can help people understand supply chain performance and make better-informed decisions.

## What I Worked On

The analysis covers ten business questions, including:

- How well are orders being delivered?
- Which shipping modes have better delivery performance?
- Which product categories and departments generate stronger sales?
- How do customer segments contribute to sales?
- Which regions and markets generate the most sales?
- How do actual shipping times compare with scheduled delivery times?
- What patterns can be identified in late deliveries?
- How might monthly order volumes change over the following 12 months?

## Tools Used

| Tool | How I used it |
|---|---|
| KNIME Analytics Platform | Data preparation, business analysis, prediction and forecasting workflows |
| Microsoft Power BI | Interactive reporting, KPI monitoring and data visualisation |
| Microsoft Excel | Data inspection and supporting analysis |
| CSV | Storage and exchange of datasets and analytical results |

## How the Project Was Built

I organised the work into four KNIME workflows.

### 1. Data Preparation

**Workflow:** `WF01_Data_Preparation`

Prepared the supply chain dataset for analysis by standardising column names, adjusting data types, converting date fields and removing unnecessary columns.

### 2. Descriptive Analytics

**Workflow:** `WF02_Descriptive_Analytics`

Answered ten business questions covering delivery performance, shipping modes, product categories, customer segments, regional sales, departments, markets and monthly order trends.

### 3. Late Delivery Prediction

**Workflow:** `WF03_Late_Delivery_Prediction`

Built a machine learning workflow to assess late-delivery risk using order, product, customer and shipping-related information.

### 4. Order Volume Forecasting

**Workflow:** `WF04_Order_Volume_Forecasting`

Used ARIMA time-series models to forecast monthly order volumes for a 12-month period, from February 2018 to January 2019.

## Power BI Report

I developed a five-page Power BI report to present the analytical results in a clear, business-focused format.

| Report page | What it covers |
|---|---|
| Executive Overview | Overall supply chain and business performance |
| Logistics Performance | Shipping methods and delivery performance |
| Supply Chain Performance | Sales across products, departments, regions and markets |
| Late Delivery Prediction | Delivery risk analysis and model evaluation |
| Order Volume Forecast | Historical order volumes and forecast comparison |

## Forecast Model Evaluation

I evaluated two ARIMA configurations using a seven-month holdout period.

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| ARIMA (1,1,1) | 228.62 | 286.40 | 11.00% |
| ARIMA (1,2,1) | 243.93 | 303.02 | 11.75% |

ARIMA (1,1,1) achieved the lower MAE, RMSE and MAPE in this evaluation. Based on these results, it was the better-performing of the two models on the holdout data.

The evaluation period was limited to seven months, so the results should be interpreted within that context.

## Project Files

The repository contains:

- Four KNIME workflows.
- The prepared supply chain dataset.
- Ten business analysis outputs.
- Late-delivery prediction results.
- Monthly order volume forecasts.
- Forecast model evaluation metrics.
- The Power BI report and supporting screenshots.

## What This Project Demonstrates

Through this project, I applied:

- Data preparation and transformation.
- Exploratory and descriptive data analysis.
- Business performance reporting.
- Supply chain and logistics analysis.
- Machine learning workflow development.
- Time-series forecasting and model evaluation.
- Interactive dashboard development using Power BI.

## Data Privacy

The original dataset contains customer-related information. Raw customer data and personally identifiable information are not intended for public distribution. Repository files are subject to privacy checks before publication.

---

**Project:** DATACO Supply Chain Analytics  
**Tools:** KNIME Analytics Platform, Microsoft Power BI, Excel  
**Focus:** Supply Chain, Logistics, Business Intelligence and Predictive Analytics
