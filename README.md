Climate DataOps Pipeline
Execution Flow
Security Setup: Enter your Kaggle API key into the Databricks text widget to securely set environment variables.

Ingestion: The script fetches data via the Kaggle API, loads it into a Pandas buffer to bypass filesystem restrictions, and converts it to a Spark DataFrame.

Medallion Pipeline:

Bronze: Data is appended in 5 batches.

Silver: Deduplication and outlier removal are performed.

Gold: Lag features are generated for time-series forecasting.

Assumptions
Temporal Order: It is assumed that data is sorted by date before batching to maintain time-series integrity.

Data Frequency: The pipeline assumes daily climate readings from the Delhi dataset.

Security & Reproducibility
Credentials are never hard-coded; they are managed via Databricks secrets/widgets.

Versioning: The pipeline's history can be audited using %sql DESCRIBE HISTORY weather_bronze.
