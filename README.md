# Housing Affordability Analytics

A hands-on analytics engineering tutorial that builds a complete workflow from a public API to SQL Server and ultimately to exploratory data analysis in Python.

The project is centered on one business question:

> **How affordable is the U.S. housing market when considering home prices, mortgage rates, housing supply, and household purchasing power?**

Rather than beginning with charts or a pre-cleaned dataset, this project starts at the source and follows the data through ingestion, transformation, modeling, validation, and analysis.

---

## Why This Project?

Analytics starts with a question.

The tools and architecture may change from project to project, but the underlying workflow is generally consistent:

```text
Business Problem
      ↓
Required Data
      ↓
Data Ingestion
      ↓
Cleaning & Standardization
      ↓
Transformation & Business Logic
      ↓
Business-Ready Data
      ↓
Analysis
      ↓
Decision Support
```

This repository documents that workflow from beginning to end using real public housing and economic data.

The goal is not only to produce an EDA. It is to understand how data moves from an external source into a trusted analytical dataset and why each layer of that process exists.

---

# Business Problem

Housing affordability cannot be understood from home prices alone.

A home may become more expensive because prices increase, but affordability can also deteriorate when mortgage rates rise, housing supply becomes constrained, or household income fails to keep pace with housing costs.

This project will investigate affordability through four primary components:

### Home Prices

How have U.S. home prices changed over time?

### Mortgage Rates

How has the cost of borrowing changed, and how might higher or lower rates affect the cost of purchasing a home?

### Housing Supply

How has housing availability changed over time, and what relationship might supply conditions have with prices?

### Household Purchasing Power

How have household incomes changed relative to housing costs?

Together, these measures provide a more complete view of housing affordability than any individual metric.

---

# Analytical Question

The primary V1 question is:

> **How affordable is the U.S. housing market based on home prices, mortgage rates, housing supply, and household purchasing power?**

Supporting questions will emerge during the analysis, including:

- How have home prices changed over time?
- How have mortgage rates changed the cost of financing a home?
- How has housing supply changed?
- Has household purchasing power kept pace with housing costs?
- During which periods did affordability conditions improve or deteriorate?
- Do changes in supply, rates, and prices appear to move together?
- Which factors appear most closely associated with major affordability shifts?

These questions will guide both the data model and the eventual EDA.

---

# Data Source

The initial source for the project is the **Federal Reserve Economic Data (FRED) API**, maintained by the Federal Reserve Bank of St. Louis.

FRED provides historical economic time-series data covering housing, interest rates, income, employment, inflation, and many other economic indicators.

For this project, the API will provide selected series representing the four components of the affordability framework:

```text
FRED
│
├── Home Price Data
├── Mortgage Rate Data
├── Housing Supply Data
└── Household Income / Purchasing Power Data
```

The exact FRED series will be selected and documented before ingestion begins.

---

# Project Architecture

The V1 architecture intentionally uses a straightforward local analytics stack so the complete data lifecycle can be understood.

```text
                     FRED REST API
                           │
                           ▼
                    Python Ingestion
                           │
                           ▼
                       SQL Server
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
             RAW       STAGING      TRANSFORM
                                         │
                                         ▼
                                        MART
                                         │
                                         ▼
                              Python / pandas
                                         │
                                         ▼
                                       EDA
                                         │
                                         ▼
                                Business Findings
```

### Technology Stack

| Component | Technology |
| --- | --- |
| Data Source | FRED REST API |
| Ingestion | Python |
| Database | Microsoft SQL Server |
| Data Transformation | SQL |
| Analytical Modeling | SQL Server |
| Exploratory Analysis | Python / pandas |
| Development Environment | VS Code / Jupyter |
| Visualization | Matplotlib |
| Version Control | Git / GitHub |

The architecture may expand in future versions, but V1 intentionally focuses on understanding the core analytical workflow before introducing additional infrastructure.

---

# Tutorial Structure

The project is organized into three major tutorials.

## Part 1 — API to SQL Server

The first section focuses on getting external data reliably into the analytical environment.

Topics will include:

- Understanding the FRED API
- Selecting economic series
- Managing API credentials
- Making REST API requests with Python
- Inspecting JSON responses
- Connecting Python to SQL Server
- Designing the raw landing layer
- Loading API observations
- Adding ingestion metadata
- Validating the load

**Goal:** reliably move source data from FRED into SQL Server while preserving source fidelity.

---

## Part 2 — Raw to Business-Ready Data

Once the source data has been ingested, the second section will focus on transforming it into reliable analytical data.

The SQL Server pipeline will follow four logical layers:

```text
RAW
 │
 ▼
STAGING
 │
 ▼
TRANSFORM
 │
 ▼
MART
```

### Raw

Preserves source data as close to its original representation as practical.

### Staging

Standardizes names, data types, dates, missing values, and other source-specific formatting.

### Transform

Applies reusable analytical logic such as period alignment, growth calculations, rolling measures, and affordability-related metrics.

### Mart

Publishes stable business-ready data designed for downstream analysis.

**Goal:** create a trusted analytical dataset so downstream users do not need to repeatedly clean and reconstruct source data.

---

## Part 3 — Housing Affordability EDA

The final section will connect Python directly to the validated SQL Server mart.

The notebook will investigate the original business question through:

- Data validation
- Descriptive analysis
- Time-series trends
- Year-over-year and period-over-period changes
- Relationships between affordability factors
- Investigation of unusual periods
- Visualizations
- Business interpretation
- Limitations
- Future analytical questions

The notebook will consume business-ready data rather than repeat transformations that belong in the SQL pipeline.

**Goal:** turn trusted analytical data into evidence that helps answer the housing affordability question.

---

# Data Quality Philosophy

Data validation will occur throughout the pipeline rather than only before analysis.

Each layer answers a different quality question:

| Layer | Validation Question |
| --- | --- |
| Raw | Did we ingest what the source returned? |
| Staging | Is the source data structurally reliable and consistently typed? |
| Transform | Did our analytical logic behave as intended? |
| Mart | Is the final dataset trustworthy at its declared grain? |

Examples include row-count reconciliation, null checks, duplicate investigation, data-type validation, grain validation, join-cardinality checks, and validation of calculated metrics.

A successful SQL query does not automatically mean the resulting data is correct.

---

# Repository Structure

```text
housing-affordability-analytics/
│
├── README.md
├── requirements.txt
│
├── ingestion/
│   └── README.md
│
├── sql/
│   ├── 01_raw/
│   ├── 02_staging/
│   ├── 03_transform/
│   └── 04_marts/
│
├── notebooks/
│   └── README.md
│
├── docs/
│   ├── architecture.md
│   ├── data_dictionary.md
│   ├── data_quality.md
│   └── findings.md
│
└── tests/
    └── README.md
```

The repository will grow alongside the tutorial. Code, validation queries, screenshots, and documentation will be added as each stage is completed.

---

# Current Status

### Phase 0 — Project Definition ✅

Completed:

- Defined the business problem
- Defined the primary analytical question
- Established the affordability framework
- Selected FRED as the initial public data source
- Defined the high-level architecture
- Defined the Raw → Staging → Transform → Mart workflow
- Established the repository and documentation structure
- Defined the initial data-quality philosophy

### Next Step

**Part 1: FRED API → SQL Server**

The next stage begins by setting up the SQL Server analytical environment and then inspecting the FRED API data that will populate the raw layer.

No ingestion or analytical transformations have been implemented yet.
