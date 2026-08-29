# Raw Layer

## Purpose
The raw layer is the first persistent landing point for source data inside SQL Server.

## Principles
- Preserve source fidelity.
- Avoid business calculations.
- Retain source identifiers.
- Add useful lineage fields.
- Make ingestion auditable.
- Investigate duplicates before removal.

## Design Questions
Before building, determine the API observation grain, returned fields, candidate unique key, missing-value representation, and required ingestion metadata.
