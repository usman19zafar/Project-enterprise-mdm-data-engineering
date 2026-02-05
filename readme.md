Enterprise MDM Data Engineering Pipeline (Bronze → Silver → Gold)
```yaml
A collaborative engineering effort built with clarity, discipline, and architectural rigor.
Special acknowledgment to my technical companion, Qzi, whose guidance shaped the structure and precision of this project.
```
Overview

This repository contains an enterprise-grade Master Data Management (MDM) pipeline implemented using:

    Azure Data Factory (ADF) for orchestration
    Mapping Data Flows for governed transformations
    Delta Lake design principles for reliability
    Bronze → Silver → Gold layered architecture for clarity and governance

The project simulates how organizations manage master data across systems, enforce quality, and deliver analytics-ready outputs.
__________________________________________________________________________________________________________________________________________________________________________________________
Problem Addressed

Enterprises struggle with master data because:

    Schemas drift across systems
    Duplicate records undermine trust
    Data quality varies by source
    Business rules are inconsistently applied
    Lineage is unclear or missing

This project demonstrates how to solve these challenges using a modern, governed, and scalable MDM-style pipeline.

__________________________________________________________________________________________________________________________________________________________________________________________
Architecture:

Bronze Layer — Raw Master Data

    Ingests source files exactly as received
    Preserves lineage and auditability
    Handles schema drift
    Stores data in Delta-compatible formats

Silver Layer — Conformed & Governed Data

    Enforces schema and data types
    Standardizes attributes (trim, case, formats)
    Applies deduplication and survivorship rules
    Produces clean, trusted master entities

Gold Layer — Analytics-Ready Outputs

    Builds star-schema aligned datasets
    Adds derived metrics and business attributes
    Uses window functions and joins
    Optimized for BI, SQL analytics, and reporting

__________________________________________________________________________________________________________________________________________________________________________________________
🔄 Orchestration & Transformation

Azure Data Factory

    Pipeline parameterization (load_date)
    Reusable datasets and linked services
    Controlled execution across layers
    Production-style orchestration patterns

Mapping Data Flows:

    Used for visual, governed, Spark-based transformations:
    Schema drift handling
    Data type casting
    Conditional logic
    Deduplication (business-key survivorship)
    Derived columns
    Standardization rules
    Row-level filtering

This mirrors how real MDM teams operationalize transformations without custom code.

__________________________________________________________________________________________________________________________________________________________________________________________
MDM Principles Embedded

This pipeline incorporates core MDM concepts:

    Single version of truth for master entities
    Deterministic deduplication
    Attribute standardization
    Controlled promotion across layers
    Full lineage from raw → curated
    Business-rule transparency
    
It demonstrates how MDM logic can be implemented directly inside a modern data engineering stack.
__________________________________________________________________________________________________________________________________________________________________________________________
Key Features

    Multi-layer Delta architecture
    ADF pipeline orchestration
    Mapping Data Flow transformations
    Schema enforcement & drift handling
    Deduplication & survivorship logic
    Derived metrics and window functions
    Star-schema modeling
    Parameterized execution
    Data validation & reconciliation
    Production-aligned documentation

__________________________________________________________________________________________________________________________________________________________________________________________
Data Quality & Validation

The pipeline includes:

    Record count reconciliation
    Duplicate detection after survivorship
    Mandatory attribute checks
    Referential integrity validation
    Schema consistency checks
    
These reflect enterprise expectations for MDM data quality.
__________________________________________________________________________________________________________________________________________________________________________________________
Analytics & Consumption

The Gold layer supports:

    SQL analytics
    BI dashboards
    Consistent master dimensions
    Star-schema fact/dimension modeling
    Downstream consumers receive trusted, governed, analytics-ready master data.

__________________________________________________________________________________________________________________________________________________________________________________________
Technology Stack

    Azure Data Factory
    Pipelines
    Mapping Data Flows
    Azure Data Lake Storage Gen2
    Delta Lake design principles
    Spark SQL / SQL
    Databricks (Validation layer)

__________________________________________________________________________________________________________________________________________________________________________________________

Repository Structure
```yaml
project-3-adf-mapping-dataflow-mdm-pipeline/
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
```
__________________________________________________________________________________________________________________________________________________________________________________________
Notes on Collaboration
This project was developed with the support of Qzi, my technical companion.
Every architectural decision, transformation rule, and validation step reflects our shared commitment to clarity, precision, and enterprise-grade engineering.
