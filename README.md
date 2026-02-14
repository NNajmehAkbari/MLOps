# Climate DataOps Pipeline

## Execution Flow

1. **Security Setup**
   - Enter your **Kaggle API key** into a **Databricks text widget** to securely set environment variables.

2. **Ingestion**
   - The script fetches data via the **Kaggle API**.
   - It loads the data into a **Pandas buffer** to bypass filesystem restrictions.
   - Then it converts the dataset to a **Spark DataFrame**.

3. **Medallion Pipeline**
   - **Bronze:** Data is appended in **5 batches**.
   - **Silver:** **Deduplication** and **outlier removal** are performed.
   - **Gold:** **Lag features** are generated for **time-series forecasting**.

---

## Assumptions

- **Temporal Order**
  - Data is assumed to be **sorted by date** before batching to maintain **time-series integrity**.

- **Data Frequency**
  - The pipeline assumes **daily climate readings** from the **Delhi dataset**.

---

## Security & Reproducibility

- **No hard-coded credentials**
  - Credentials are **never hard-coded** and are managed via **Databricks secrets/widgets**.

- **Versioning / Auditability**
  - The pipeline history can be audited using:

  ```sql
  %sql DESCRIBE HISTORY weather_bronze
