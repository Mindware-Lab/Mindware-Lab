# Data Pipeline Component

Purpose:
- ingest cognitive app telemetry
- enforce schema validation
- produce analysis-ready tables

Inputs:
- task events
- session metadata
- participant metadata (pseudonymized)

Outputs:
- cleaned event tables
- feature tables for modeling
- reproducible analysis notebooks