# Ingestion

## Purpose
Python will retrieve selected FRED API observations and load them into the SQL Server raw layer.

## Responsibilities
- Authenticate without exposing credentials.
- Request intended series and observation ranges.
- Validate request success.
- Preserve source identifiers.
- Add ingestion metadata.
- Load raw records.
- Surface failures rather than silently skipping them.

## Design Principle
Complex cleaning and business logic should not occur during ingestion. The goal is reliable source-to-raw movement with enough fidelity for troubleshooting and reproducibility.

## Credentials
API keys and database credentials must not be committed. Local secrets will use environment variables or a local `.env` excluded from Git.

## Current Status
Not yet implemented. SQL Server configuration and source inspection come first.
