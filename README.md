# SmartDemand-AI

**An End-to-End Machine Learning Project for Retail Demand Forecasting**

## Overview

SmartDemand-AI is a machine learning project focused on retail demand forecasting using historical grocery sales data.

The project aims to analyze historical sales patterns, identify factors influencing product demand, and develop predictive models that can forecast future sales across multiple stores and product families.

The ultimate goal is to build a practical forecasting solution that can support better inventory planning, demand estimation, and data-driven business decisions.

## Business Problem

Accurate demand forecasting is an important challenge in retail.

Overestimating demand can lead to excess inventory and increased storage costs, while underestimating demand can result in stockouts, lost sales, and poor customer experiences.

SmartDemand-AI explores how historical sales, promotional activities, store characteristics, transactions, holidays, and external economic indicators can be used to improve demand forecasting.

## Dataset

The project uses the **Store Sales - Time Series Forecasting** dataset from Kaggle, based on sales data from Corporación Favorita, an Ecuadorian grocery retailer.

The dataset contains historical sales information across multiple stores and product families, along with additional information that may influence demand.

For a detailed explanation of the dataset, its files, and columns, see [DATASET.md](<DATASET.md>).

**Dataset source:** [Kaggle – Store Sales: Time Series Forecasting](<https://www.kaggle.com/competitions/store-sales-time-series-forecasting/data>)

## Project Objectives

- Perform exploratory data analysis (EDA) to understand sales patterns and distributions.
- Investigate temporal, promotional, geographical, and economic factors affecting demand.
- Prepare and consolidate data from multiple sources.
- Engineer meaningful features for time-series forecasting.
- Develop and compare machine learning models.
- Evaluate model performance using time-based validation.
- Build a dashboard for visualizing forecasts and business insights.
- Explore deployment and MLOps practices for a reproducible ML workflow.

## Technology Stack

| Category | Technologies |
| --- | --- |
| Programming | Python |
| Data manipulation | Pandas, NumPy |
| Data visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Data storage | CSV, Parquet |
| Development | Jupyter Notebook, VS Code |
| Version control | Git, GitHub |

Additional technologies will be introduced as the project progresses.

## Repository Structure

``` text
SmartDemand-AI/
│
├── data/
│   ├── raw/                 # Original datasets
│   └── processed/           # Consolidated and processed data
│
├── notebooks/
│   ├── 01_data_exploration_and_consolidation.ipynb
│   ├── 02_feature_engineering.ipynb
│   └── 03_model_training_and_evaluation.ipynb
│
├── src/                     # Reusable Python modules
│
├── README.md
├── DATASET.md
├── requirements.txt
└── .gitignore
```

Raw and processed datasets are excluded from version control because of their size. Refer to DATASET.md for instructions on obtaining the original data.

## Development Roadmap

The project is being developed incrementally, with an emphasis on understanding each stage rather than simply training a model.

- [x] Dataset exploration and initial analysis
- [x] Data consolidation and integration
- [ ] Feature engineering
- [ ] Data preprocessing and preparation
- [ ] Machine learning model development
- [ ] Model evaluation and comparison
- [ ] Forecast visualization dashboard
- [ ] API development
- [ ] Experiment tracking and model management
- [ ] Cloud deployment and MLOps

## Current Status

**Current phase: Data Exploration and Consolidation Completed**

The initial exploration and consolidation stages have been completed.

The consolidated training dataset currently contains 3,000,888 records and 23 columns, combining sales information with transaction data, oil prices, store metadata, and holiday-related features.

The next stage focuses on feature engineering and preparing the dataset for time-series forecasting.

## Project Philosophy

This project emphasizes:

- Reproducible data preparation.
- Proper time-series validation and prevention of data leakage.
- Meaningful feature engineering.
- Model evaluation based on business-relevant metrics.
- Clean, modular, and maintainable code.
- Progressive development toward an end-to-end machine learning system.

---

**Project:** SmartDemand-AI  
**Status:** In Development  
**Language:** Python