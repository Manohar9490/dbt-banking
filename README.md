# 🏦 Banking Data Platform: End-to-End Modern Data Stack

> A comprehensive data engineering ecosystem for real-time banking transactions — built with CDC, Kafka, MinIO, Airflow, Snowflake, and dbt.

---

## 📌 Table of Contents

- [Architecture Overview](#architecture-overview)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Data Modeling (dbt)](#data-modeling-dbt)
- [Author](#author)

---

## 🏗️ Architecture Overview

| Layer               | Technology                  | Role                                                         |
| ------------------- | --------------------------- | ------------------------------------------------------------ |
| **Source Database** | PostgreSQL 15               | Transactional DB with logical WAL for CDC                    |
| **Ingestion (CDC)** | Debezium via Kafka Connect  | Captures row-level Inserts, Updates, Deletes                 |
| **Message Broker**  | Confluent Kafka & Zookeeper | High-throughput event streaming                              |
| **Data Lake**       | MinIO (S3-compatible)       | Landing zone for raw JSON events                             |
| **Orchestration**   | Apache Airflow 2.x          | Automates MinIO → Snowflake movement & dbt snapshots         |
| **Transformation**  | dbt (Data Build Tool)       | Medallion architecture (Bronze → Silver → Gold) in Snowflake |

---

## 🚀 Key Features

- **Real-time Event Streaming** — Captures database changes instantly to keep the data warehouse always up-to-date.
- **SCD Type 2 History** — Implemented via dbt snapshots to track historical changes in customer and account status.
- **Infrastructure as Code** — Fully containerized with Docker for one-click reproducibility.
- **Advanced Modeling** — Modular dbt models including `dim_customers`, `dim_accounts`, and `fact_transactions`.

---

## 📂 Project Structure

```
├── banking/                 # dbt project root
│   ├── models/              # SQL transformations (staging, marts, dimensions)
│   ├── snapshots/           # SCD Type 2 logic for accounts and customers
│   └── dbt_project.yml      # dbt configuration
├── docker/                  # Infrastructure configurations
│   └── dags/                # Airflow DAGs for data pipeline orchestration
├── consumers/               # Python scripts for Kafka-to-MinIO ingestion
├── data-generator/          # Script to simulate live banking traffic
├── docker-compose.yml       # Orchestration file for the full stack
└── requirements.txt         # Python library dependencies
```

---

## 🛠️ Setup & Installation

### 1️⃣ Prerequisites

- [Docker & Docker Compose](https://docs.docker.com/compose/install/)
- Python 3.10+: (Recommended)_ [`uv`](https://github.com/astral-sh/uv) for fast dependency management
- A [Snowflake](https://www.snowflake.com/) account

---

### 2️⃣ Environment Setup

Create a `.env` file in the root directory to store sensitive credentials.

```env
# Airflow UI
AIRFLOW_WWW_USER=admin
AIRFLOW_WWW_USER_PASSWORD=admin

# Databases
POSTGRES_USER=postgres_user
POSTGRES_PASSWORD=postgres_pass
AIRFLOW_DB_USER=airflow_user
AIRFLOW_DB_PASSWORD=airflow_pass

# MinIO
MINIO_ROOT_USER=minio_admin
MINIO_ROOT_PASSWORD=minio_password
```

---

### 3️⃣ Execution

Spin up the entire platform with a single command:

```bash
docker-compose up -d
```

Once running, access the services at:

| Service           | URL                   |
| ----------------- | --------------------- |
| Airflow Webserver | http://localhost:8080 |
| MinIO Console     | http://localhost:9001 |
| Kafka Connect API | http://localhost:8083 |

---

## 📊 Data Modeling (dbt)

The warehouse logic follows a professional **Medallion** tier structure:

| Layer       | Models                              | Description                                             |
| ----------- | ----------------------------------- | ------------------------------------------------------- |
| **Staging** | `stg_customers`, `stg_transactions` | Cleans and standardizes raw source data from PostgreSQL |
| **Marts**   | `dim_accounts`, `dim_customers`     | Business-ready dimension tables                         |
| **Fact**    | `fact_transactions`                 | Analytical reporting and financial tracking             |

> SCD Type 2 history is maintained via dbt snapshots, ensuring full auditability of customer and account changes over time.

---

## 👨‍💻 Author

**Manohar Killamsetti**

- 🎓 MS in Computer Science, Pace University _(Expected May 2026)_
- 📍 New Jersey / New York Area
- 💼 6+ years in Data & Analytics Engineering (Amazon, Cognizant, Tech Mahindra)
- 🌐 [GitHub](https://github.com/manohar9490) · [LinkedIn](https://linkedin.com/in/manohar-killamsetti)

---

_Built with ❤️ using the Modern Data Stack._
