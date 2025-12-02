# 2019 US Imports – trade.csv Schema (Draft)

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
```

Data Assumptions:
Each row represents a single trade flow for a given year, origin, destination, and industry pair.
Region1 and region2 may use short country/region codes.
Amount is recorded in a consistent currency (e.g., USD).
There should be no duplicate rows for the same trade_id.

Example Analysis Queries:
1. Total US import value by exporting country:
```sql
SELECT region1, SUM(amount) AS total_import_value
FROM trade_imports_2019
GROUP BY region1
ORDER BY total_import_value DESC;
```

2. Top 10 imported industries into the US:
```sql
SELECT industry2, SUM(amount) AS total_import_value
FROM trade_imports_2019
GROUP BY industry2
ORDER BY total_import_value DESC
LIMIT 10;
```

3. Imports by year and industry pair:
```sql
SELECT year, industry1, industry2, SUM(amount) AS total_import_value
FROM trade_imports_2019
GROUP BY year, industry1, industry2
ORDER BY year, total_import_value DESC;
``` 



