# Enterprise MDM Data Engineering Pipeline  
### Bronze → Silver → Gold Architecture

A collaborative engineering effort built with clarity, discipline, and architectural rigor.

---

## Overview

This repository contains an **enterprise-grade Master Data Management (MDM) data engineering pipeline**
implemented using:

- **Azure Data Factory (ADF)** for orchestration  
- **Mapping Data Flows** for governed, scalable transformations  
- **Delta Lake design principles** for reliability and traceability  
- **Bronze → Silver → Gold layered architecture** for clarity and governance  

The project simulates how organizations manage master data across systems, enforce quality standards,
and deliver analytics-ready outputs in a production-aligned environment.

---

## Problem Addressed

Enterprises struggle with master data because:

- Schemas drift across operational systems  
- Duplicate records undermine trust  
- Data quality varies by source  
- Business rules are inconsistently applied  
- Lineage is unclear or missing  

This project demonstrates how to address these challenges using a **modern, governed, and scalable
MDM-style data engineering pipeline**.

---

## Architecture

### Bronze Layer — Raw Master Data
- Ingests source files exactly as received  
- Preserves lineage and auditability  
- Handles schema drift explicitly  
- Stores data in Delta-compatible formats  

### Silver Layer — Conformed & Governed Data
- Enforces schema and data types  
- Standardizes attributes (trim, case, formats)  
- Applies deterministic deduplication and survivorship rules  
- Produces clean, trusted master entities  

### Gold Layer — Analytics-Ready Outputs
- Builds star-schema aligned datasets  
- Adds derived metrics and business attributes  
- Uses window functions and joins  
- Optimized for BI, SQL analytics, and reporting  

---

## Orchestration & Transformation

### Azure Data Factory
- Pipeline parameterization (e.g., `load_date`)  
- Reusable datasets and linked services  
- Controlled execution across layers  
- Production-style orchestration patterns  

### Mapping Data Flows
Mapping Data Flows are used for **visual, governed, Spark-based transformations**, including:

- Schema drift handling  
- Data type casting  
- Conditional logic  
- Deduplication using business-key survivorship  
- Derived columns  
- Attribute standardization rules  
- Row-level filtering  

This mirrors how real-world MDM teams operationalize transformation logic without custom code.

---

## MDM Principles Embedded

This pipeline incorporates core **MDM design principles**, including:

- Single version of truth for master entities  
- Deterministic deduplication and survivorship  
- Attribute standardization and validation  
- Controlled promotion across Bronze → Silver → Gold layers  
- Full lineage from raw ingestion to curated outputs  
- Transparent, auditable business rules  

It demonstrates how MDM logic can be implemented **directly within a modern data engineering stack**.

---

## Key Features

- Multi-layer Delta-style architecture  
- ADF pipeline orchestration  
- Mapping Data Flow–based transformations  
- Schema enforcement and drift handling  
- Deduplication and survivorship logic  
- Derived metrics and window functions  
- Star-schema modeling  
- Parameterized execution  
- Data validation and reconciliation  
- Production-aligned documentation  

---

## Data Quality & Validation

The pipeline includes enterprise-grade validation checks such as:

- Record count reconciliation across layers  
- Duplicate detection after survivorship  
- Mandatory attribute completeness checks  
- Referential integrity validation  
- Schema consistency enforcement  

These checks reflect **real-world MDM data quality expectations**.

---

## Analytics & Consumption

The Gold layer supports:

- SQL analytics  
- BI dashboards  
- Consistent master dimensions  
- Star-schema fact and dimension modeling  

Downstream consumers receive **trusted, governed, analytics-ready master data**.

---

## Technology Stack

- Azure Data Factory  
  - Pipelines  
  - Mapping Data Flows  
- Azure Data Lake Storage Gen2  
- Delta Lake design principles  
- Spark SQL / SQL  
- Databricks (validation and analytics)

---

## Repository Structure

```text
enterprise-mdm-data-engineering/
│
├── README.md
├── architecture/
│   ├── high-level-architecture.png
│   ├── dataflow-diagram.png
│   └── layer-diagram.png
│
├── adf/
│   ├── pipeline/
│   ├── dataflows/
│   ├── datasets/
│   └── linked-services/
│
├── databricks/
│   ├── notebooks/
│   └── sql/
│
├── data/
│   ├── raw/
│   └── clean/
│
└── docs/
    ├── business-rules.md
    ├── transformation-rules.md
    ├── deduplication-logic.md
    ├── parameterization.md
    └── validation-checks.md
