## Hands_on_L9_Streaming Analytics with Spark

**Cloud Computing for Data Analysis (ITCS 6190/8190, Fall 2025)**  
Instructor: *Marco Vieira*<br />
Name: *Manish Yendeti*<br />  
ID: *801429980*

---

## Overview
This project builds a real-time ride-sharing analytics system using Apache Spark Structured Streaming.  
It includes three Spark streaming tasks and a Python data generator that continuously produces JSON ride data.

---

## Project Structure
```
Handson-L8-Spark-SQL_Streaming/
├── outputs/
│   ├── task1_outputs/
│   ├── task2_outputs/
│   └── task3_outputs/
├── data_generator.py
├── task1.py
├── task2.py
├── task3.py
├── requirements.txt
├── .gitignore
└── README.md
```

---

## Tasks
**Task 1 – Basic Streaming Ingestion and Parsing**
- Reads data from `localhost:9999`
- Converts JSON strings into structured columns
- Displays parsed data live on the console

**Task 2 – Real-Time Aggregations (Driver-Level)**
- Groups by `driver_id` to calculate:
  - Total fare amount (`SUM(fare_amount)`)
  - Average distance (`AVG(distance_km)`)
- Continuously writes the results as CSV files to `outputs/task2_outputs/`

**Task 3 – Windowed Time-Based Analytics**
- Converts timestamp values into proper `TimestampType`
- Performs a 5-minute rolling aggregation on `fare_amount`, sliding every 1 minute and watermarking by 1 minute
- Saves the final output in `outputs/task3_outputs/`

---

## Running the Project
```bash
pip install pyspark
python data_generator.py    # Start data stream generator
python task1.py             # Run this in another terminal
python task2.py             # Execute for real-time aggregations
python task3.py             # Execute for time-window analysis
```

After running, check the `outputs/` directory. Each task folder includes multiple Spark output files (`part-...csv`) and `_SUCCESS` indicators.

---

## Approach, Results, and Observations

### Approach
- The system follows a **producer-consumer** design.  
  The `data_generator.py` acts as the data producer, while Spark jobs consume and analyze data in real time.  
- Spark Structured Streaming is used for data parsing, aggregations, and time-based analytics.

---

### Results Summary
- **Task 1:** Successfully parsed and printed live JSON ride data.  
- **Task 2:** Produced per-driver total fare and average distance in real-time CSV outputs.  
- **Task 3:** Computed rolling fare totals using 5-minute windows and 1-minute slides.

---

### Observations
- Spark requires checkpoint directories (`/tmp/checkpoints/`) for consistent streaming state management.  
- Task 3 needs several minutes of execution to fill a complete 5-minute window before generating results.  
- The output structure (multiple part files and `_SUCCESS` files) matches Spark’s expected streaming format.  
- The repository layout and file naming follow the submission standards exactly.
