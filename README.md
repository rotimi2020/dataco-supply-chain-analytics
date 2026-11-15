# DATACO Supply Chain Analytics

**Supply Chain Analytics | KNIME | Power BI | Machine Learning | Time-Series Forecasting**

## About the Project

How well is a supply chain performing? Where are delivery delays happening, which shipping methods perform better, and what can historical order data tell us about future demand?

This project explores these questions using the DataCo supply chain dataset. I used KNIME to prepare and analyse the data, investigate business performance, develop a late-delivery prediction workflow and forecast monthly order volumes. I then brought the findings together in a five-page Power BI report.

The focus was not simply on producing charts, but on turning operational data into meaningful insights that help explain supply chain performance, identify potential issues and support better-informed business decisions.

## What I Worked On

The descriptive analysis (WF02) addresses ten business questions across delivery performance, logistics, sales and order trends.

1. **Overall Delivery Performance**  
   What percentage of order items are delivered late, on time, shipped in advance, or cancelled?

2. **Shipping Mode Performance**  
   Which shipping modes have the highest number of late deliveries, and how do their late-delivery rates compare?

3. **Product Category Profitability**  
   Which product categories generate the highest sales revenue and recorded profit, and which categories perform poorly?

4. **Customer Segment Performance**  
   Which customer segments generate the highest sales revenue?

5. **Regional Sales Performance**  
   Which order regions generate the highest and lowest sales revenue?

6. **Late Delivery Rate by Shipping Mode**  
   Which shipping mode has the highest late-delivery rate after accounting for the number of order items handled by each mode?

7. **Department Performance**  
   Which departments contribute the most to total sales revenue?

8. **Market Performance**  
   Which markets generate the highest and lowest sales revenue?

9. **Actual vs. Scheduled Shipping Time**  
   How do actual shipping times compare with scheduled shipping times, and how often do deliveries take longer than expected?

10. **Monthly Sales Trend**  
    How does sales revenue change from month to month, and are there noticeable increases, decreases, or seasonal patterns?

The corresponding analysis outputs are available in the processed-data folder.

**[Explore the processed dataset and analysis outputs](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/data/processed)**

## Tools Used

| Tool | How I used it |
|---|---|
| KNIME Analytics Platform | Data preparation, descriptive analysis, machine learning and forecasting workflows |
| Microsoft Power BI | Interactive reporting, KPI monitoring and data visualisation |
| Microsoft Excel | Data inspection and supporting analysis |
| CSV | Storage and exchange of datasets and analytical results |

## How the Project Was Built

I organised the analytical work into four KNIME workflows, each addressing a different stage of the project.

### 1. Data Preparation

**Workflow:** `WF01_Data_Preparation`

Prepared the supply chain dataset for analysis by standardising column names, adjusting data types, converting date fields, filtering unnecessary columns and exporting the cleaned dataset.

### 2. Descriptive Analytics

**Workflow:** `WF02_Descriptive_Analytics`

Investigated the ten business questions covering delivery performance, shipping modes, product categories, customer segments, regional sales, departments, markets, shipping times and monthly sales trends.

### 3. Late Delivery Prediction

**Workflow:** `WF03_Late_Delivery_Prediction`

Developed and evaluated a machine-learning workflow to assess late-delivery risk using available order, product, customer and shipping features.

### 4. Order Volume Forecasting

**Workflow:** `WF04_Order_Volume_Forecasting`

Used ARIMA time-series models to forecast monthly unique order volume for a 12-month period, from February 2018 to January 2019.

**[Explore all four KNIME workflows](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/knime)**

## Power BI Report

I developed a five-page Power BI report to bring the analytical findings together in an interactive, business-focused format.

| Report page | What it covers |
|---|---|
| Executive Overview | Overall supply chain and business performance |
| Logistics Performance | Shipping methods and delivery performance |
| Supply Chain Performance | Sales across products, departments, regions and markets |
| Late Delivery Prediction | Delivery risk analysis and model evaluation |
| Order Volume Forecast | Historical order volumes and forecast comparison |

### Report Screenshots

The following images provide a preview of the report and its key analytical pages.

#### 1. Executive Overview

![DATACO Executive Overview](powerbi/screenshots/01_Executive_Overview.PNG)

#### 2. Logistics Performance

![DATACO Logistics Performance](powerbi/screenshots/02_Logistics_Performance.PNG)

#### 3. Supply Chain Performance

![DATACO Supply Chain Performance](powerbi/screenshots/03_Supply_Chain_Performance.PNG)

#### 4. Late Delivery Prediction

![DATACO Late Delivery Prediction](powerbi/screenshots/04_Late_Delivery_Prediction.PNG)

#### 5. Order Volume Forecast

![DATACO Order Volume Forecast](powerbi/screenshots/05_Order_Volume_Forecast.PNG)

**[Explore the Power BI project files](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/powerbi)**

## Forecast Model Evaluation

I evaluated two ARIMA configurations using a seven-month holdout period.

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| ARIMA (1,1,1) | 228.62 | 286.40 | 11.00% |
| ARIMA (1,2,1) | 243.93 | 303.02 | 11.75% |

ARIMA (1,1,1) recorded lower MAE, RMSE and MAPE values, making it the better-performing of the two models on the evaluation data.

The evaluation was based on a seven-month holdout period, so the results should be interpreted within that limitation.

## Project Files

The repository is organised to make the project materials easy to explore.

- **KNIME:** Four workflows covering preparation, descriptive analytics, prediction and forecasting.
- **Processed Data:** The prepared dataset and ten business analysis outputs.
- **Prediction Results:** Late-delivery prediction outputs.
- **Forecasting:** Monthly order-volume forecasts and model evaluation metrics.
- **Power BI:** The report files and supporting screenshots.

The project folders provide access to the relevant materials:

- [Processed data and analysis outputs](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/data/processed)
- [Four KNIME workflows](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/knime)
- [Power BI report files and screenshots](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/powerbi)

## What This Project Demonstrates

Through this project, I applied:

- Data preparation, cleaning and transformation.
- Exploratory and descriptive data analysis.
- Supply chain and logistics performance analysis.
- Business performance reporting and KPI monitoring.
- Machine-learning workflow development.
- Late-delivery risk analysis.
- Time-series forecasting and model evaluation.
- Interactive dashboard development using Power BI.

## Data Privacy

The original dataset contains customer-related information. Raw data containing personally identifiable information is not intended for public distribution. The repository focuses on reviewed project materials and analytical outputs.

---

**Project:** DATACO Supply Chain Analytics  
**Tools:** KNIME Analytics Platform | Microsoft Power BI | Excel  
**Focus:** Supply Chain | Logistics | Business Intelligence | Predictive Analytics | Forecasting
