# Data Dictionary

## Status
This is a living document. Exact fields will be added after the selected FRED series are inspected and the raw SQL Server schema is designed.

## Planned Source Categories

| Category | Analytical Purpose |
| --- | --- |
| Home Prices | Measure the cost of purchasing housing |
| Mortgage Rates | Measure the cost of borrowing |
| Housing Supply | Measure availability or supply pressure |
| Household Purchasing Power | Provide income context for housing costs |

## Planned Technical Metadata
Potential ingestion metadata includes `source_system`, `series_id`, and `ingestion_timestamp`. Final names and data types will be documented after implementation.

## Grain
Grain will be documented separately for each layer. The provisional V1 analytical grain is one row per reporting period for the national U.S. housing market, subject to source-frequency review.
