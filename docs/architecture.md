# Architecture

## Purpose
This project uses a layered analytics architecture to turn public housing and economic data into trusted, analysis-ready information.

**Business problem → source data → ingestion → raw → staging → transformation → mart → analysis → decision support**

## Initial Technology Stack
- Source: Federal Reserve Economic Data (FRED) API
- Ingestion: Python
- Database: Microsoft SQL Server
- Transformation: SQL
- Analysis: Python, pandas, Jupyter notebooks in VS Code
- Version control and documentation: GitHub

## Data Flow
```text
FRED REST API
      |
      v
Python ingestion
      |
      v
SQL Server
      |
      +--> raw
      |     Preserve source records and ingestion metadata
      |
      +--> staging
      |     Standardize fields, types, dates, and null handling
      |
      +--> transform
      |     Align measures and apply reusable analytical logic
      |
      +--> mart
            Publish analysis-ready affordability data
                  |
                  v
          Python / pandas
                  |
                  v
        Exploratory Data Analysis
                  |
                  v
            Business Findings
```

## Layer Responsibilities
### Raw
Preserve source fidelity, source identifiers, and ingestion metadata. Avoid business calculations.

### Staging
Standardize names, types, dates, null handling, and source-specific representations. Investigate duplicates and establish structurally reliable records.

### Transform
Create reusable analytical logic such as period-over-period changes, rolling measures, ratios, and aligned time grains.

### Mart
Publish stable analysis-ready datasets. The V1 grain will be finalized after source frequencies are confirmed; a likely starting grain is one row per reporting period for the national U.S. housing market.

## Why Layers?
Separating ingestion, cleanup, business logic, and consumption improves traceability, testing, maintainability, and reuse.

## Future Extensions
Future versions may add geographic dimensions, Power BI, orchestration, incremental ingestion, centralized logging/observability, cloud storage and compute, and automated CI/CD tests.
