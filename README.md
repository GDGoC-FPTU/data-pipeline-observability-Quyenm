# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** anhquyen9a10a@gmail.com
**Name:** Nguyễn Mạnh Quyền 

---

## Description

This lab builds an ETL pipeline that automatically reads product data from a JSON file, performs data quality validation, transforms the data, and outputs it to a CSV file. The pipeline removes records with invalid prices or empty categories, applies a 10% discount to prices, standardizes category names, and adds a processing timestamp.

In addition, this lab includes a Stress Test experiment to observe how "dirty" data affects the responses of an AI Agent.

---

## How to Run

### Prerequisites

```bash
pip install pandas
```

### Run ETL Pipeline

```bash
python solution.py
```

After running, check that the file `processed_data.csv` has been created.

### Generate Garbage Data

```bash
python generate_garbage.py
```

### Run Agent Simulation (Stress Test)

Run the agent with clean data first, then with garbage data:

```bash
python agent_simulation.py
```

The agent will compare responses using `processed_data.csv` (clean data) and `garbage_data.csv` (poisoned data).

---

## Project Structure

```
├── solution.py              # ETL Pipeline script (Extract, Validate, Transform, Load)
├── generate_garbage.py      # Script to generate garbage_data.csv for stress testing
├── agent_simulation.py      # AI Agent simulation with two datasets
├── raw_data.json            # Source data (5 records, 2 invalid)
├── processed_data.csv       # Pipeline output (3 valid records)
├── experiment_report.md     # Experiment report: Clean vs Garbage data
└── README.md                # This file
```

---

## Results

* Total input records: **5**
* Valid records (processed): **3** *(Laptop, Chair, Monitor)*
* Removed records: **2**

### Removed Record Details:

* Record `id=3` (Mystery Box): negative price (-10) → violates rule `price > 0`
* Record `id=4` (Phone): empty category → violates rule that category must not be empty

---

## Output

The file `processed_data.csv` contains the following columns:

* `id`
* `product`
* `price`
* `category`
* `discounted_price`
* `processed_at`
