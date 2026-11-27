# Dataset Documentation

## 1. Dataset Overview

SmartDemand-AI uses the **Store Sales - Time Series Forecasting** dataset published on Kaggle.

The dataset originates from Corporación Favorita, a large grocery retailer operating in Ecuador.

It was provided as part of a Kaggle forecasting competition, where the objective was to predict future product-family sales across multiple stores.

**Source:** [Kaggle – Store Sales: Time Series Forecasting](https://www.kaggle.com/competitions/store-sales-time-series-forecasting/data)

The dataset contains historical sales records and several supplementary datasets describing store characteristics, promotions, transactions, holidays, and oil prices.

## 2. Dataset Files

The original competition dataset contains several CSV files.

| File | Description |
|---|---|
| `train.csv` | Historical sales records used for model training. |
| `test.csv` | Records for which sales predictions are required. |
| `stores.csv` | Store metadata, including location and store classification. |
| `oil.csv` | Daily crude oil price information. |
| `holidays_events.csv` | Holidays, events, and related calendar information. |
| `transactions.csv` | Daily transaction counts for individual stores. |
| `sample_submission.csv` | Example submission format for the competition. |

## 3. Training Dataset (`train.csv`)

The training dataset contains historical sales observations for different product families across multiple stores.

**Dataset dimensions:**

- Rows: 3,000,888
- Columns: 6
- Stores: 54
- Product families: 33
- Unique dates: 1,684
- Date range: January 1, 2013 – August 15, 2017

### Columns

| Column | Description | Data type |
|---|---|---|
| `id` | Unique identifier for each sales observation. | Integer |
| `date` | Date of the sales observation. | Datetime |
| `store_nbr` | Identifier of the store. | Integer |
| `family` | Product family associated with the observation. | String |
| `sales` | Number of units sold for the corresponding store, date, and product family. | Float |
| `onpromotion` | Number of items in the product family that were on promotion at the store on that date. | Integer |

**Target variable:** `sales`

The objective is to predict future sales for each store and product-family combination.

## 4. Supplementary Datasets

### 4.1 Stores (`stores.csv`)

Contains information describing the stores.

| Column | Description |
|---|---|
| `store_nbr` | Unique store identifier. |
| `city` | City where the store is located. |
| `state` | State where the store is located. |
| `type` | Store classification. |
| `cluster` | Grouping of similar stores. |

Dataset dimensions: 54 rows and 5 columns.

### 4.2 Oil Prices (`oil.csv`)

Contains daily crude oil price observations.

| Column | Description |
|---|---|
| `date` | Observation date. |
| `dcoilwtico` | Daily oil price indicator. |

Oil prices can provide additional economic context that may be useful for understanding changes in retail demand.

The original dataset contains missing values and does not include every calendar date.

During preparation, missing observations were handled through chronological forward filling after aligning the oil data with the training dates.

### 4.3 Holidays and Events (`holidays_events.csv`)

Contains information about holidays and special events.

| Column | Description |
|---|---|
| `date` | Date of the holiday or event. |
| `type` | Holiday or event classification. |
| `locale` | Geographic scope: National, Regional, or Local. |
| `locale_name` | Name of the corresponding geographic location. |
| `description` | Description of the holiday or event. |
| `transferred` | Indicates whether the holiday was transferred to another date. |

Multiple records can exist for the same date because different holidays or events may occur simultaneously or apply to different geographical areas.

### 4.4 Transactions (`transactions.csv`)

Contains the number of transactions recorded at individual stores on specific dates.

| Column | Description |
|---|---|
| `date` | Transaction date. |
| `store_nbr` | Store identifier. |
| `transactions` | Number of transactions recorded at the store on that date. |

Transactions are store-level observations rather than product-family-level observations.

Therefore, this dataset is joined to sales records using both `date` and `store_nbr`.

### 4.5 Test Dataset (`test.csv`)

Contains the store-date-product-family combinations for which predictions are required.

It follows the same general structure as the training dataset, excluding the target variable `sales`.

## 5. Exploratory Data Analysis

Initial exploration was performed to understand the structure and characteristics of the training data.

Some observations included:

- Sales values are highly skewed.
- A large number of observations contain zero sales.
- December has the highest average monthly sales.
- February has the lowest average monthly sales.
- Grocery I, Beverages, and Produce are among the highest-selling product families.
- Sales patterns vary across product families and months.

These observations will guide the subsequent feature engineering and modeling stages.

## 6. Data Preparation and Consolidation

The supplementary datasets were processed and integrated into a consolidated training dataset.

### Operations performed

1. Converted date columns into appropriate datetime types.
2. Investigated missing values and duplicate records.
3. Aligned oil prices with the training calendar.
4. Integrated store transaction counts using `date` and `store_nbr`.
5. Created general holiday and event indicators.
6. Created geographical holiday indicators using:
   - National holidays.
   - Regional holidays matching store states.
   - Local holidays matching store cities.
7. Integrated store metadata.
8. Validated the consolidated dataset for row preservation and duplicate keys.

### Consolidated dataset

The resulting DataFrame is named `train_features`.

| Property | Value |
|---|---:|
| Rows | 3,000,888 |
| Columns | 23 |
| Unique IDs | 3,000,888 |
| Duplicate date-store-family combinations | 0 |

The consolidated dataset includes:

- Original sales information.
- Store metadata.
- Oil prices.
- Transaction counts.
- General holiday indicators.
- National, regional, and local holiday indicators.

### Missing Transaction Values

The consolidated dataset contains 245,784 missing transaction values, corresponding to 7,448 unique store-date combinations.

These missing values have been preserved rather than automatically replaced with zero, since missing transaction records do not necessarily indicate zero transactions.

Their treatment will be evaluated during the preprocessing and modeling stages.

## 7. Processed Data Storage

The consolidated dataset is stored locally in Parquet format:

```text
data/
├── raw/
│   └── Original Kaggle CSV files
│
└── processed/
    └── train_features.parquet
```

Parquet was selected because it offers efficient storage and loading for large tabular datasets while preserving column data types.

Raw and processed datasets are excluded from Git version control.

## 8. Dataset Usage and Reproducibility

To reproduce the project:

1. Obtain the original competition data from Kaggle.
2. Place the downloaded CSV files in `data/raw/`.
3. Install the project dependencies.
4. Execute the data exploration and consolidation notebook.
5. Generate the consolidated Parquet dataset.

Refer to the main [README.md](README.md) for the project overview and development roadmap.

---

**Dataset:** Store Sales - Time Series Forecasting  
**Organization:** Corporación Favorita  
**Source:** Kaggle  
**Project:** SmartDemand-AI