# Transformation Layer

## Purpose
Apply reusable analytical and business logic to standardized source data.

## Potential V1 Logic
- Align series to a common time grain.
- Calculate MoM and YoY changes.
- Calculate rolling measures.
- Create affordability-related ratios.
- Prepare reusable intermediate datasets.

Calculations reused by notebooks, dashboards, or future products should generally live in the transformation pipeline rather than be recreated downstream.
