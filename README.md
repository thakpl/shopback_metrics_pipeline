# SELF-SERVING-CUSTOMER-METRICS

A simple prototype system to automate the definition, validation, and calculation of data metrics using YAML and DuckDB.

## Setup instructions

**1. Install Dependencies**
Ensure you have Python installed on your system. Open your terminal at the root of the project and install the required libraries:

```bash
pip install duckdb pyyaml pandas

```

**2. Prepare the Data**
Make sure the `data/` directory contains the required CSV files: `customers.csv`, `orders.csv`, and `order_items.csv`.

**3. Run the Pipeline**
Execute the main script from the root directory to initialize the database, load the CSVs, and calculate the existing metrics:

```bash
python src/run_metrics.py

```

*(This will generate a `metrics.duckdb` file and print a sample of the data to your console).*

---

## How to add a new metric

**Step 1: Create a YAML file**
Navigate to the `metrics/` folder and create a new `.yaml` file (e.g., `new_metric.yaml`).

**Step 2: Define the metric**
Populate the file with the required metadata and SQL logic. Follow this standard structure:

```yaml
metric_name: your_metric_table_name
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

**Step 3: Validate the metric**
Run the validation script to ensure your YAML file has all required keys and valid syntax:

```bash
python src/validate_yaml.py

```

*Check the console output. If it reports missing keys or errors, fix them before proceeding.*

**Step 4: Execute the metric**
Once the validation passes, run the main script to execute the SQL and create/replace the table in DuckDB:

```bash
python src/run_metrics.py

```

---

## Development guideline

**Updating the Scripts**

* **Validation Logic:** If you need to add new mandatory metadata fields (like data types or tags) or implement advanced SQL parsing, update the validation logic inside `src/validate_yaml.py`.
* **Execution Logic:** To modify how DuckDB connects, handles initial CSV ingestion, or executes queries, update the functions inside `src/run_metrics.py`.

**Running Unit Tests**
Currently, the YAML validation acts as our primary configuration test suite. To test your metric definitions before deployment, always run:

```bash
python src/validate_yaml.py

```

*Note for future scaling: If you plan to add testing frameworks like `pytest` to test the internal Python functions (e.g., mocking the database connection), you should create a separate `tests/` directory and execute `pytest` from the root folder.*
