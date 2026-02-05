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

ROW_NUMBER() OVER (PARTITION BY business_key ORDER BY last_updated DESC

- Keep only `row_number = 1`.

---

## 3. Gold Layer Transformations

### 3.1 Customer Dimension
- Aggregate orders to compute:
- total_revenue
- total_quantity
- order_count
- avg_order_value

### 3.2 Product Dimension
- Standardize product attributes.
- Compute product-level metrics if required.

### 3.3 Fact Orders
- Join Silver Orders with Silver Customers and Silver Products.
- Produce star-schema fact table.

### 3.4 Order Metrics Table
- Use window functions:
- `LAG(total_amount)` to compute previous order value
- `RANK()` for customer ranking
- Produce analytics-ready metrics.

---

## 4. Output Format
- All outputs stored as Delta-compatible files.
- Partitioning by `load_date` where applicable.
