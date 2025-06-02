# Debezium CDC Pipeline

A simple change data capture (CDC) pipeline that captures PostgreSQL changes using Debezium, streams them via Kafka, processes them with Vector, and persists into ClickHouse.

## Tech Stack

- Postgres
- Debezium
- Kafka
- Vector
- ClickHouse

## Data Flow

Postgres (change) → Debezium → Kafka → Vector → ClickHouse

## Getting Started

### 1. Create Source Table in Postgres

```sql
CREATE TABLE IF NOT EXISTS demo_table (
  id SERIAL PRIMARY KEY,
  message VARCHAR(255) NOT NULL
);
```

### 2. Register Debezium Connector

```bash
curl -X POST http://localhost:8083/connectors \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d @debezium.json
```

### 3. Create Destination Table in ClickHouse

```sql
CREATE TABLE IF NOT EXISTS demo (
  id Int32,
  message String
) ENGINE = MergeTree()
ORDER BY id;
```

### 4. Insert Test Data

```sql
INSERT INTO demo_table (message) VALUES ('Message');
```