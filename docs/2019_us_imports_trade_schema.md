# 2019 US Imports – trade.csv Schema (Draft)

This document describes the draft SQL schema for the `trade.csv` file in:

`trade-data/year/2019/US/imports/trade.csv`

## CSV Columns

The main columns in `trade.csv` are:

- `trade_id`   – unique identifier for each trade flow record
- `year`       – year of the trade data (e.g., 2019)
- `region1`    – source/exporting region or country
- `region2`    – destination/importing region or country (US in this case)
- `industry1`  – exporting industry/sector in region1
- `industry2`  – destination industry/sector in region2
- `amount`     – trade value (numeric amount)

## Draft SQL Table Definition

A possible SQL table for this dataset:

```sql
CREATE TABLE trade_imports_2019 (
    trade_id INT PRIMARY KEY,
    year INT,
    region1 VARCHAR(10),      -- exporting country
    region2 VARCHAR(10),      -- importing country (US)
    industry1 VARCHAR(255),   -- source industry
    industry2 VARCHAR(255),   -- destination industry
    amount NUMERIC(20,4)      -- trade value
);
