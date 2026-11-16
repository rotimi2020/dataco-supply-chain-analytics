# DATACO Supply Chain Analytics

**Supply Chain Analytics | KNIME | Power BI | Machine Learning | Time-Series Forecasting**

## About the Project

How well is a supply chain performing? Where are delivery delays happening, which shipping methods perform better, and what can historical order data tell us about future demand?

This project explores those questions using the DataCo Smart Supply Chain dataset. I used KNIME to prepare and analyse the data, investigate delivery and commercial performance, build an exploratory late-delivery classifier and test monthly order-volume forecasts. I then brought the findings together in a five-page Power BI report.

The aim was to make the analysis useful to someone making operational decisions—not just to produce charts. The results highlight where performance deserves a closer look, while being clear about the limits of the data and models.

### Power BI report preview

The Executive Overview is shown first so visitors can see the reporting style immediately.

![DATACO Executive Overview](powerbi/screenshots/01_Executive_Overview.PNG)

[Explore the Power BI report files and all five page previews](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/powerbi).

## At a Glance

This analysis covers **180,519 order-item records across 65,752 orders**. The clearest finding is a **54.83% late-delivery rate** at order-item level, with First Class showing the highest recorded late rate (**95.32%**). A Random Forest workflow identifies **91.41%** of records labelled late in its test export, but its F1 score does not outperform a simple always-late benchmark. The two ARIMA configurations tested also trail a previous-month diagnostic baseline. The project therefore focuses on what the data reveals, what the models can—and cannot—support, and where further operational investigation is justified.

## Table of Contents

- [Key Findings](#key-findings)
- [Project Overview](#project-overview)
- [What I Worked On](#what-i-worked-on)
- [Tools and Technologies](#tools-and-technologies)
- [How the Project Was Built](#how-the-project-was-built)
- [Power BI Report](#power-bi-report)
- [Recommendations](#recommendations)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [What This Project Demonstrates](#what-this-project-demonstrates)
- [Dataset Source and Attribution](#dataset-source-and-attribution)
- [Data and Privacy](#data-and-privacy)
- [About the Author](#about-the-author)

## Key Findings

### Delivery and logistics

The prepared dataset contains **180,519 order-item records across 65,752 distinct orders**. At order-item level, the recorded delivery outcomes are:

| Delivery status | Order items | Share |
|---|---:|---:|
| Late delivery | 98,977 | 54.83% |
| Advance shipping | 41,592 | 23.04% |
| Shipping on time | 32,196 | 17.83% |
| Shipping cancelled | 7,754 | 4.30% |

More than half of the records are labelled late. That is the clearest service-performance issue in this dataset. These percentages describe recorded order-item outcomes, not unique orders.

Shipping-mode results are not what a reader might expect from the service labels:

| Shipping mode | Late-delivery rate |
|---|---:|
| First Class | **95.32%** |
| Second Class | **76.63%** |
| Same Day | **45.74%** |
| Standard Class | **38.07%** |

First Class has the highest late-delivery rate and Standard Class the lowest. This is an association in the historical data, not proof that the shipping mode caused the delay. The rates include the dataset's cancelled records in the mode totals; keep that denominator in mind when interpreting comparisons.


### Regional and commercial picture

Central Africa has the highest regional late-delivery rate at **57.96%**, followed by South Asia at **56.27%**. Canada has the lowest rate at **48.80%**. The difference is about 9.16 percentage points, although even the lowest-rate region has a substantial late share.

By recorded sales, **Western Europe** leads at approximately **5.89 million**, followed by **Central America** at **5.67 million**. **Central Asia** has the lowest regional sales total at approximately **109,840**. The supplied project documentation does not establish a reporting currency, so these are presented as dataset sales units rather than assigned a currency.

Consumer customers account for approximately **19.10 million** in sales, ahead of Corporate (**11.17 million**) and Home Office (**6.52 million**). Europe is the largest market by sales at approximately **10.87 million**, narrowly ahead of LATAM (**10.28 million**). Fan Shop is the largest department by recorded sales at approximately **17.11 million**.


### Late-delivery model

The KNIME workflow uses a **Random Forest classifier with 100 trees**. It partitions 180,519 records into 144,415 training rows (80%) and 36,104 test rows (20%). The exported test predictions produce these metrics when compared with the actual target labels:

| Metric | Test-set result |
|---|---:|
| Accuracy | 58.18% |
| Precision | 57.54% |
| Recall | 91.41% |
| F1 score | 70.63% |

The model catches a high share of records labelled late, but it also flags many records that were not late. On this test set, it correctly identifies about **17.58% of the non-late records**. For context, an always-late classifier would achieve **55.00% accuracy, 55.00% precision, 100% recall and 70.96% F1**. The Random Forest improves accuracy and precision, but its **70.63% F1 is slightly below that simple baseline**. This makes it an exploratory risk-screening result rather than a model to use for operational decisions. Treat it as exploratory risk screening, not a deployment-ready model.

The selected predictors include scheduled shipping days, shipping mode, quantity, sales, product price, discounts, market, region, transaction type, category, department, customer segment, year and day of week. The target is `Late_delivery_risk`. The workflow's column filter excludes actual shipping days and `Delivery Status`, reducing two obvious forms of post-outcome leakage. However, the partition is stratified by **Category Name**, not by the target column. The reported results should therefore be read as an exploratory assessment.

### Forecast evaluation

The forecasting work produced a useful comparison rather than a claim that one model is universally reliable. On the seven-month holdout period, ARIMA (1,1,1) performed better than ARIMA (1,2,1):

- **ARIMA (1,1,1):** MAE 228.62 | RMSE 286.40 | MAPE 11.00%
- **ARIMA (1,2,1):** MAE 243.93 | RMSE 303.02 | MAPE 11.75%

I also calculated a simple **previous-month baseline** from the actual monthly volumes in the evaluation file. For the six months where a preceding month was available (August 2017–January 2018), carrying the previous month's actual volume forward gives a MAPE of **4.43%**. This baseline is materially better than either ARIMA result on those six observations. It is not a like-for-like seven-month comparison, so it should be treated as a diagnostic rather than a definitive model ranking. It does show why a simple benchmark matters before presenting a forecast model as useful.

**What this means:** the ARIMA (1,1,1) model is the stronger of the two ARIMA configurations tested, but the current evidence does not show that it beats a simple naïve forecast. The forecasting workflow needs further tuning and validation before it should guide operational decisions.

## Project Overview

The project combines descriptive analytics, predictive modelling and time-series forecasting to examine different aspects of supply chain performance.

The main objectives were to:

- Prepare and standardise supply chain data for analysis.
- Evaluate delivery performance and identify shipping-related patterns.
- Compare sales performance across products, customers, departments, regions and markets.
- Develop a machine-learning workflow to assess late-delivery risk.
- Forecast monthly unique order volume using ARIMA models.
- Present analytical findings through an interactive Power BI report.

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

The corresponding prepared dataset and analysis outputs are available in the repository. The numerical findings should be read alongside the definitions and denominators used in each analysis.

**[Explore the processed dataset and analysis outputs](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/data/processed)**

## Tools and Technologies

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

Built a Random Forest classifier with 100 trees to estimate `Late_delivery_risk`. The workflow uses an 80/20 partition and exports predictions for 36,104 test records. On that export, accuracy is 58.18%, precision 57.54%, recall 91.41% and F1 70.63%. Actual shipping days and delivery status are excluded from the selected predictor columns. The workflow is presented as an exploratory assessment of late-delivery risk.

### 4. Order Volume Forecasting

**Workflow:** `WF04_Order_Volume_Forecasting`

Tested two ARIMA configurations to forecast monthly unique order volume for February 2018 to January 2019. The available evaluation file covers a seven-month holdout period; a simple previous-month baseline was also checked separately as a diagnostic.

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

### Other report pages

| Logistics Performance | Supply Chain Performance |
|---|---|
| ![DATACO Logistics Performance](powerbi/screenshots/02_Logistics_Performance.PNG) | ![DATACO Supply Chain Performance](powerbi/screenshots/03_Supply_Chain_Performance.PNG) |

| Late Delivery Prediction | Order Volume Forecast |
|---|---|
| ![DATACO Late Delivery Prediction](powerbi/screenshots/04_Late_Delivery_Prediction.PNG) | ![DATACO Order Volume Forecast](powerbi/screenshots/05_Order_Volume_Forecast.PNG) |

**[Explore the Power BI project files](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/powerbi)**

## Recommendations

The results point to a few practical questions worth taking back to an operations team:

- **Review First Class exceptions first.** Its 95.32% late rate warrants a closer look at routes, order mix, promised delivery windows and service assignment. The result alone is not a reason to move volume into another mode.
- **Separate service failures from cancellations.** Recalculate mode-level delivery rates excluding cancelled records as a sensitivity check, then compare both versions.
- **Investigate regional variation.** Start with Central Africa and South Asia, the two highest-rate regions in the analysis, but compare shipment volumes, product mix, shipping mode and scheduled delivery windows before attributing the difference to geography.
- **Use the classifier as a review queue, not an automatic decision.** Its high recall may help flag orders for attention, but its modest precision means teams would also review many orders that are not late.
- **Keep forecasting honest.** ARIMA (1,1,1) is the better of the two ARIMA configurations tested, but the separate previous-month diagnostic performed better on its six comparable transitions. More validation is needed before relying on the 12-month forecast.

These are recommendations for investigation based on the observed results, not claims of savings or improvements already achieved.

## Repository Structure

The repository is organised to make the project materials easy to explore.

```text
dataco-supply-chain-analytics/
│
├── data/
│   └── processed/
│       ├── Prepared supply chain dataset
│       ├── Q01–Q10 analysis outputs
│       ├── Late delivery predictions
│       └── Order volume forecasts and model evaluation
│
├── documentation/
│   └── Project documentation and business questions
│
├── knime/
│   ├── WF01_Data_Preparation.knwf
│   ├── WF02_Descriptive_Analytics.knwf
│   ├── WF03_Late_Delivery_Prediction.knwf
│   └── WF04_Order_Volume_Forecasting.knwf
│
├── powerbi/
│   ├── Power BI report files
│   └── screenshots/
│       ├── 01_Executive_Overview.PNG
│       ├── 02_Logistics_Performance.PNG
│       ├── 03_Supply_Chain_Performance.PNG
│       ├── 04_Late_Delivery_Prediction.PNG
│       └── 05_Order_Volume_Forecast.PNG
│
└── README.md
```

The project folders provide access to the relevant materials:

- [Project documentation](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/documentation)

- [Processed data and analysis outputs](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/data/processed)
- [Four KNIME workflows](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/knime)
- [Power BI report files and screenshots](https://github.com/rotimi2020/dataco-supply-chain-analytics/tree/main/powerbi)

## Getting Started

You can explore the project using the following tools:

1. **KNIME Analytics Platform:** Open the KNIME workflow files in the `knime` folder to inspect the data preparation, descriptive analysis, prediction and forecasting processes.
2. **Microsoft Power BI Desktop:** Open the available `.pbix` report in the `powerbi` folder to explore the interactive dashboards.
3. **Microsoft Excel:** Open the available analysis files to inspect the supporting business-question outputs.
4. **CSV files:** Review the prepared dataset and analytical results in the `data/processed` folder.

To reproduce the analysis from the source data, download the dataset from the [Kaggle page](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis) or use the [original Mendeley Data record](https://data.mendeley.com/datasets/8gx2fvg2k6/5). Open `WF01_Data_Preparation` first and check its input-file location before running it. The workflow's local file path may need to be updated for your machine. The repository does not yet specify the KNIME version or the extensions used to run the workflows.

The project files are available directly through the repository links above. No separate application installation or deployment is required to explore the supplied reports and outputs, although the relevant desktop software is needed to open its native files.

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
- Translation of analytical findings into business-focused reporting.

## Dataset Source and Attribution

I downloaded the dataset from the [Kaggle copy uploaded by Shashwat Tiwari](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis). Kaggle is the download location I used; the original dataset record is published on Mendeley Data by **Fabian Constante, Fernando Silva and António Pereira (2019)**.

**Original dataset citation:** Constante, F., Silva, F. and Pereira, A. (2019). *DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS* (Version 5). Mendeley Data. https://doi.org/10.17632/8gx2fvg2k6.5

The Mendeley Data record identifies the dataset as **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Reuse must retain appropriate attribution, provide the licence link and indicate changes where applicable. This attribution applies to the dataset as identified in that Mendeley record; it does not automatically license my analysis code, dashboard design or other project materials.

## Data and Privacy

This repository contains project materials, a prepared dataset and analytical outputs; it is not a copy of the full original download package. The source data includes customer-related fields, so I have not included the raw download as a public repository asset. Anyone reproducing the analysis should obtain the dataset from its cited source, review the fields before sharing any extracts, and avoid publishing identifiable customer information.

## About the Author

**Rotimi S. Omosewo**

Data and Reporting Analyst | Operations and Supply Chain Analytics

I am interested in using data analysis, business intelligence and reporting to understand operational performance and support evidence-based decisions.

[GitHub Profile](https://github.com/rotimi2020)

---

**Project:** DATACO Supply Chain Analytics  
**Tools:** KNIME Analytics Platform | Microsoft Power BI | Excel  
**Focus:** Supply Chain | Logistics | Business Intelligence | Predictive Analytics | Forecasting
