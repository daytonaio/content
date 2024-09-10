---
title: "Setting Up a DuckDB Playground with Daytona"
description: "Learn how to create a DuckDB playground using Daytona and DevContainers for hands-on analytical processing experiments."
date: 2024-08-23
author: "David Anyatonwu"
tags: ["duckdb", "daytona", "devcontainers", "data-analysis", "python"]
---

# Setting Up a DuckDB Playground with Daytona

## Introduction

DuckDB is an innovative analytical database system that combines the simplicity of SQLite with the power of column-oriented data processing. It's designed for fast in-memory analytics on structured data, making it an excellent choice for data scientists, analysts, and backend developers working with large datasets([Duckdb docs](https://duckdb.org/docs/)).

This guide is perfect for:
- Data analysts and scientists looking to supercharge their analytical workflows
- Backend developers curious about high-performance, in-process databases
- Anyone eager to explore the cutting edge of data processing technology

We'll walk you through setting up a DuckDB playground environment using Daytona, a Development Environment Manager, and DevContainers. This setup will allow you to experiment with DuckDB's features and capabilities in a controlled, reproducible environment.

### Why DuckDB? The Analytical Powerhouse

DuckDB isn't just another database - it's a game-changer for analytical processing([Why DuckDB?](https://duckdb.org/why_duckdb)):

1. **Lightning-fast in-memory processing**: DuckDB operates primarily in-memory, resulting in blazing-fast query execution.
2. **Columnar storage for the win**: This design is optimized for analytical queries, allowing for efficient data compression and faster scans.
3. **Vectorized query execution**: DuckDB processes data in batches, leveraging modern CPU architectures for mind-blowing performance.
4. **SQL you know and love**: It supports a wide range of SQL commands, making it feel like home for SQL aficionados.
5. **Python's new best friend**: DuckDB can directly query Pandas DataFrames and Arrow tables without data copies, seamlessly integrating into your data science workflow.

### TL;DR

- **Create a GitHub repository** for your DuckDB playground
- **Set up a Daytona workspace** with DuckDB and Python
- **Explore DuckDB features** through CLI and Python examples
- **Experiment with data processing** using DuckDB's powerful analytical capabilities

## Step 1: Creating the GitHub Repository

Let's kick things off by creating a new GitHub repository for our DuckDB playground:

1. Log in to your GitHub account
2. Click on the '+' icon in the top-right corner and select 'New repository'
3. Name your repository "playground-duckdb"
4. Initialize it with a README.md file
5. Click 'Create repository'

## Step 2: Setting Up the Daytona Workspace

Now, let's create a Daytona workspace for our DuckDB playground. You may use this template repository as a starting point.

1. Open your terminal and run the following command:

```bash
daytona create https://github.com/onyedikachi-david/playground-duckdb.git --code
```
2. This both creates the repository and opens the workspace in your preferred IDE.

## Step 3: Configuring the DevContainer

To ensure a consistent development environment, we'll use a DevContainer configuration. Create a new file `.devcontainer/devcontainer.json` in your repository with the following content:

```json
{
  "name": "DuckDB Playground",
  "build": {
    "dockerfile": "../Dockerfile",
    "context": "..",
    "args": {
      "VARIANT": "3.10-bullseye",
      "NODE_VERSION": "lts/*"
    }
  },
  "features": {
    "ghcr.io/eitsupi/devcontainer-features/duckdb-cli:1": {}
  },
  "customizations": {
    "vscode": {
      "settings": {
        "python.defaultInterpreterPath": "/usr/local/bin/python",
        "python.linting.enabled": true,
        "python.linting.pylintEnabled": true,
        "python.formatting.autopep8Path": "/usr/local/py-utils/bin/autopep8",
        "python.formatting.blackPath": "/usr/local/py-utils/bin/black",
        "python.formatting.yapfPath": "/usr/local/py-utils/bin/yapf",
        "python.linting.banditPath": "/usr/local/py-utils/bin/bandit",
        "python.linting.flake8Path": "/usr/local/py-utils/bin/flake8",
        "python.linting.mypyPath": "/usr/local/py-utils/bin/mypy",
        "python.linting.pycodestylePath": "/usr/local/py-utils/bin/pycodestyle",
        "python.linting.pydocstylePath": "/usr/local/py-utils/bin/pydocstyle",
        "python.linting.pylintPath": "/usr/local/py-utils/bin/pylint"
      }
    }
  }
}
```

This configuration sets up a Python environment with DuckDB CLI and necessary Python packages installed.

### Creating a requirements.txt file

To manage Python dependencies, create a `requirements.txt` file in the root of your project with the following content:

```txt
duckdb
pandas
matplotlib
```

This file lists the Python packages required for our DuckDB playground.

## Project Structure

After setting up your DuckDB playground, your project structure should look like this:

```
playground-duckdb/
├── .devcontainer/
│   └── devcontainer.json
├── duckdb_example.py
├── advanced_analytics.py
├── requirements.txt
└── README.md
```

## Sample Data

To make our examples more practical, let's create a sample CSV file. Create a file named `example.csv` in your project directory with the following content:

```csv
s,x
ducks,3.14159
geese,2.71828
swans,1.41421
```

## Step 4: Exploring DuckDB Features

Now that our environment is set up, let's dive into some DuckDB magic!

### DuckDB CLI: Your New Command-Line Companion

1. Open a terminal in your Daytona workspace
2. Start the DuckDB CLI by typing `duckdb`
3. Let's try out some SQL commands with a twist:

```sql
-- Create a table with some quirky data
CREATE TABLE example (s STRING, x DOUBLE);
INSERT INTO example VALUES ('ducks', 3.14159), ('geese', 2.71828), ('swans', 1.41421);

-- Query the data
SELECT * FROM example;

-- Pretty-print those pesky floating-point numbers
SELECT s, x::DECIMAL(10, 5) AS x_pretty FROM example;
```

### Python and DuckDB: A Match Made in Data Heaven

Create a new file named `duckdb_example.py` with the following content:

```python
import duckdb
import pandas as pd

# Connect to an in-memory database
conn = duckdb.connect()

# Create a sample pandas DataFrame
bird_data = pd.DataFrame({
    "species": ["Mallard", "Wood Duck", "Gadwall", "Pintail"],
    "count": [42, 17, 9, 31]
})

# Register the DataFrame as a view in DuckDB
conn.register("bird_sightings", bird_data)

# Query the DataFrame using SQL
result = conn.execute("SELECT species FROM bird_sightings WHERE count > 20").fetchdf()
print("Birds with more than 20 sightings:")
print(result)

# Create a table and insert data
conn.execute("CREATE TABLE migration_data (species STRING, distance_km INTEGER)")
conn.execute("INSERT INTO migration_data VALUES ('Mallard', 1500), ('Wood Duck', 800), ('Gadwall', 2000), ('Pintail', 2500)")

# Join tables and query
result = conn.execute("""
    SELECT b.species, b.count, m.distance_km
    FROM bird_sightings b
    JOIN migration_data m ON b.species = m.species
    WHERE m.distance_km > 1000
    ORDER BY m.distance_km DESC
""").fetchdf()
print("\nBirds that migrate more than 1000 km:")
print(result)
```

Run this script using the command `python duckdb_example.py` to see DuckDB and Python working together in harmony.

### Advanced Analytics with Python

Let's explore some advanced analytics capabilities of DuckDB using Python. Create a new file named `advanced_analytics.py` with the following content:

```python
import duckdb
import pandas as pd

# Connect to an in-memory database
conn = duckdb.connect()

# Create a sample pandas DataFrame
data = {
    "category": ["A", "B", "C", "A", "B", "C", "A", "B", "C"],
    "value": [10, 20, 30, 40, 50, 60, 70, 80, 90]
}
df = pd.DataFrame(data)

# Register the DataFrame as a view in DuckDB
conn.register("data", df)

# Group by category and calculate the sum of values
result = conn.execute("SELECT category, SUM(value) AS sum_value FROM data GROUP BY category").fetchdf()
print("Sum of values by category:")
print(result)

# Calculate the average value for each category
result = conn.execute("SELECT category, AVG(value) AS avg_value FROM data GROUP BY category").fetchdf()
print("\nAverage value by category:")
print(result)

# Join two tables based on a common column
conn.execute("CREATE TABLE categories (category STRING, description STRING)")
conn.execute("INSERT INTO categories VALUES ('A', 'Category A'), ('B', 'Category B'), ('C', 'Category C')")

result = conn.execute("""
    SELECT d.category, d.value, c.description
    FROM data d
    JOIN categories c ON d.category = c.category
""").fetchdf()
print("\nJoined data with categories:")
print(result)
```

Run this script using the command `python advanced_analytics.py` to see DuckDB's advanced analytics capabilities in action.

## DuckDB Tricks: Unleash the Power

DuckDB has some nifty tricks up its sleeve. Let's explore a few that can supercharge your data manipulation and analysis:

1. **Pretty-printing floating-point numbers**:
   DuckDB allows for easy formatting of floating-point numbers using DECIMAL casting.
   
   ```sql
   SELECT x::DECIMAL(15, 3) AS x
   FROM 'example.csv';
   ```

   This approach is preferred over using `printf` or `format` functions as it maintains the numeric type for further operations.

2. **Copying the schema of a table**:
   You can create an empty table with the same schema as an existing table using `LIMIT 0`.
   
   ```sql
   CREATE TABLE example AS
       FROM 'example.csv';
   CREATE TABLE tbl AS
       FROM example
       LIMIT 0;
   ```

3. **Shuffling data**:
   DuckDB offers ways to shuffle data both non-deterministically and deterministically.
   
   Non-deterministic shuffling:
   ```sql
   FROM 'example.csv' ORDER BY random();
   ```
   
   Deterministic shuffling:
   ```sql
   CREATE OR REPLACE TABLE example AS FROM 'example.csv';
   FROM example ORDER BY hash(rowid + 42);
   ```

4. **Specifying types when reading CSVs**:
   DuckDB allows you to specify column types when reading CSV files, overriding auto-detection.
   
   ```sql
   CREATE OR REPLACE TABLE example AS
       FROM read_csv('example.csv', types = {'x': 'DECIMAL(15, 3)'});
   ```

5. **Updating CSV files in-place**:
   DuckDB can read, process, and write CSV files in-place.
   
   ```sql
   COPY (SELECT s FROM 'example.csv') TO 'example.csv';
   ```

   This operation is more straightforward in DuckDB compared to Unix shell commands.

6. **Compact data creation with FROM-first syntax**:
   DuckDB supports a concise way to create and populate tables in one go.
   
   ```sql
   COPY (FROM VALUES ('foo', 10/9), ('bar', 50/7), ('qux', 9/4) t(s, x))
   TO 'example.csv';
   ```

These tricks, taken directly from the DuckDB community examples, can significantly enhance your data manipulation and analysis capabilities. Experiment with them in your DuckDB playground to unlock new levels of data processing efficiency!

## Conclusion

Congratulations! You've just set up a powerful DuckDB playground using Daytona and DevContainers. We've explored some of DuckDB's key features and provided examples of both basic and advanced usage. 

As you continue your DuckDB journey, remember that you're working with a database system designed for analytical workloads. Focus your experiments on complex queries, large datasets, and integration with data science workflows. The sky's the limit with DuckDB!

For more in-depth information and advanced features, don't forget to check out the [official DuckDB documentation](https://duckdb.org/docs/). Happy data crunching!