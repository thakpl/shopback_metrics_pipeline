# Shopback Metrics Pipeline Prototype

This project is a simple prototype system that automates the process of defining, validating, and calculating data metrics using YAML and DuckDB.

## Prerequisites

To run this project, you need Python installed on your system. Please install the required dependencies using the following command:

```bash
pip install duckdb pyyaml pandas

```

## Setup Instructions

1. Unzip the project directory and open your terminal/command prompt at the root of the project.
2. Ensure the `/data` directory contains the 3 required CSV datasets (`customers.csv`, `orders.csv`, `order_items.csv`).
3. Initialize the database and calculate the default metrics by running:

```bash
python src/run_metrics.py

```

*(This script will automatically create the `metrics.duckdb` database file, load data from the CSVs into tables, and execute the SQL queries defined in the `/metrics/` folder).*

---

## How to Add a New Metric

Adding a new metric to the system is straightforward. Just follow these step-by-step instructions:

**Step 1:** Create a new `.yaml` file inside the `/metrics/` directory (e.g., `new_metric.yaml`).

**Step 2:** Fill in all the required keys and the SQL logic. Below is the standard structure you must follow:

```yaml
metric_name: target_table_name
description: A brief description of what this metric calculates
owner: data.analyst@shopback.com
schedule: "0 8 * * *"
sql: |
  SELECT 
      column_a,
      SUM(column_b) AS total
  FROM orders
  GROUP BY 1;

```

**Step 3:** Validate your newly created metric by running the following command:

```bash
python src/validate_yaml.py

```

*The system will scan your YAML file to ensure no required keys are missing and the SQL field is populated. If there are any errors, please check the terminal logs to fix them.*

**Step 4:** Once the validation is successful (the console prints "Valid and complete"), run the main script again so DuckDB can execute the SQL and create/update the new metric table:

```bash
python src/run_metrics.py

```
