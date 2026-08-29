# Tests

## Purpose
Testing verifies that the pipeline produces trustworthy data at each stage. Tests may begin as SQL validation queries and become automated later.

## Categories
- **Structural:** expected columns, types, and required values.
- **Grain:** uniqueness and join-cardinality checks.
- **Reconciliation:** compare source/raw and upstream/downstream outputs.
- **Business logic:** validate growth periods, null handling, and time alignment.
- **Reasonableness:** investigate implausible values or sudden changes.

A pipeline is not complete merely because the SQL runs; its output must be validated sufficiently to support analysis.
