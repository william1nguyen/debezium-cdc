# debezium-CDC

### Connect Debezium with Postgres

- Create `demo` table
  ```
  CREATE TABLE IF NOT EXISTS demo_table(
    id SERIAL PRIMARY KEY,
    message VARCHAR(255) NOT NULL
  )
  ```

- Register new `connector` with `debezium-connector`
  ```
  curl -X POST http://localhost:8083/connectors \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d @debezium.json
  ```


### Clickhouse support
```
-- Create the table to match your Debezium payload structure
CREATE TABLE IF NOT EXISTS demo (
    id Int32,
    message String
) ENGINE = MergeTree()
ORDER BY id;
```

### Test

- Insert new data
  ```
  INSERT INTO demo_table (message) VALUES ('Message');
  ```