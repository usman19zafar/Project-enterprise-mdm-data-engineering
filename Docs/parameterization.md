# Parameterization Strategy

This document describes how the pipeline uses parameters to support reusability, automation, and incremental processing.

---

## 1. Pipeline Parameter: load_date
- Name: `load_date`
- Type: String
- Format: `YYYY-MM-DD`
- Drives:
  - Source folder path
  - Sink folder path
  - Partitioning logic

---

## 2. Source Path Parameterization
ADF dataset path:

raw/<entity>/load_date=@{pipeline().parameters.load_date}


---

## 3. Sink Path Parameterization
ADF sink path:

clean/<entity>/load_date=@{pipeline().parameters.load_date}


---

## 4. Data Flow Parameterization
Mapping Data Flow parameter:
- `load_date` passed from pipeline

Used to:
- Filter data by date
- Write outputs to correct partition

---

## 5. Benefits
- Reusable for daily/weekly/monthly loads
- Supports incremental ingestion
- Enables backfills
- Reduces duplication of pipelines

