# Transformation Rules (Bronze → Silver → Gold)

This document describes the exact transformations applied in each layer of the MDM pipeline.

---

## 1. Bronze Layer Transformations
- Ingest raw CSV/Delta files from Blob storage.
- Preserve original schema and data types.
- Add ingestion metadata:
  - `ingestion_timestamp`
  - `source_file_name`
- No cleansing or standardization is applied here.

---

## 2. Silver Layer Transformations

### 2.1 Schema Enforcement
- Cast all fields to expected types:
  - IDs → integer/long
  - Prices → double
  - Dates → date
  - Strings → string

### 2.2 Standardization
- Trim all string fields.
- Convert:
  - names → proper case
  - emails → lowercase
  - categories → uppercase
- Standardize date formats.

### 2.3 Data Quality Filtering
- Remove rows with null business keys.
- Remove negative quantities or prices.
- Remove invalid dates.

### 2.4 Derived Columns
- `total_amount = quantity * unit_price`
- `order_year = year(order_date)`
- `order_month = month(order_date)`

### 2.5 Deduplication
- Apply window function:
