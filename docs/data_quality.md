# Data Quality Strategy

## Objective
Data quality is part of the pipeline, not a final cleanup step.

- **Raw:** Did we ingest what the source returned?
- **Staging:** Is the data structurally reliable and consistently typed?
- **Transform:** Did the analytical logic behave as intended?
- **Mart:** Is the final dataset trustworthy at its declared grain?

## Raw Checks
- Reconcile API results and loaded rows where appropriate.
- Confirm required source fields exist.
- Retain series identifiers.
- Validate observation dates and ingestion timestamps.
- Identify duplicates rather than silently deleting them.

## Staging Checks
- Parse dates successfully.
- Parse observations to appropriate numeric types.
- Standardize missing-value representations.
- Check required identifiers for nulls.
- Evaluate uniqueness at expected source grain.

## Transformation Checks
- Validate comparison periods for growth calculations.
- Ensure joins occur at compatible grains.
- Detect unintended row multiplication.
- Handle nulls and divide-by-zero safely.
- Validate ordering in window calculations.

## Mart Checks
- Uniqueness at declared grain.
- Not-null reporting keys.
- Expected period coverage.
- Valid dimension relationships where applicable.
- Reasonable ranges for analytical measures.
- Reconciliation to trusted upstream outputs.

## Duplicate Principle
Duplicates should be investigated before deletion. A duplicate may be legitimate, source-specific, ingestion-related, or a true data-quality defect.
