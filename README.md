# Credit Card Fraud Detection — Neo4j Project

**Author:** Arman Rashidizadeh  
**Date:** September 2025  
**Project:** New Generation Data Models and DBMSs

## Project Overview

This project implements a **graph-based NoSQL data model** for credit card fraud detection using **Neo4j**.  
It was developed as part of a university course on _New Generation Data Models and DBMSs_ and demonstrates how graph modeling and query optimization can support complex fraud-detection workloads efficiently.  
The goal of the project is to design and implement a **Neo4j property graph model** capable of answering analytical queries related to credit card fraud detection.  
The model is based on a simulated dataset (generated with the open-source [Fraud Detection Handbook simulator](https://fraud-detection-handbook.github.io/fraud-detection-handbook/Chapter_3_GettingStarted/SimulatedDataset.html)) and includes three main entities:

- **Customer -** properties: `CUSTOMER_ID`, `SPENDING_AMOUNT`, `SPENDING_FREQUENCY`, `AVAILABLE_TERMINALS`, etc.
- **Terminal -** properties: `TERMINAL_ID`, `LONGTITUDE`, `LATITUDE`.
- **Transaction -** properties: `TRANSACTION_ID`, `TX_DATETIME`, `TX_AMOUNT`, `TX_FRAUD`, `TX_FRAUD_SCENARIO`, etc.
  **Note:** When saving datasets to CSVs, set the `index=True`.

Key relationships:

- `(Customer)-[:MADE]->(Transaction)-[:OCCURRED_AT]->(Terminal)`
- Derived relationship `(Customer)-[:USED]->(Terminal)` used for performance optimization.
  The repository contains:
- Python scripts to **load** and **preprocess** data into Neo4j.
- Cypher script for **analytical operations** on fraud detection (e.g., co-customer relationships, anomaly detection, buying-friend detection).

## Repository Structure

```
NoSQL-Neo4j
│
├── LoadDatabase.ipynb
├── Queries.ipynb
|── requirements.txt
└── README.md
```

## Requirements

- **Neo4j Community Server** (version ≥ 5.x)
- **Python** 3.10+

## Installation

1. **Install Neo4j Community Server**  
   Download from [Neo4j Download Center](https://neo4j.com/deployment-center/#community)
2. **Clone this repository**
   ```bash
       git clone https://github.com/Arman-Rz/NoSQL-Neo4j.git
       cd NoSQL-Neo4j
   ```
3. **Install dependencies**
   ```bash
        pip install -r requirements.txt
   ```
4. **Place the dataset**  
   Copy or generate the CSV files into:
   ```arduino
       neo4j-community-202x.xx.x/import
   ```
5. **Configure Neo4j**
   - Update `neo4j.conf` to allow CSV imports:
     ```ini
         dbms.security.allow_csv_import_from_file_urls=true
     ```
   - Download and add the [apoc](https://neo4j.com/docs/apoc/current/installation/) plugin in the following directory:
     ```arduino
       neo4j-community-202x.xx.x/plugins
     ```
6. **Load CSVs into the database**  
   To do that, run the `LoadDatabase.ipynb` notebook.

7. **Run the queries**
   In the `Queries.ipynb`, you will find the initial data modifications and sample queries.

## Notes

- The data generation notebook is not included to keep the repository light, but it can be accessed [here](https://fraud-detection-handbook.github.io/fraud-detection-handbook/Chapter_3_GettingStarted/SimulatedDataset.html)
- Both scripts are designed for **local Neo4j Community Server** usage.
- Modify file paths in scrips to match your Neo4j directory structure.

## License

This project is distributed for **educational and academic use only**.  
© 2025 Arman Rashidizadeh
