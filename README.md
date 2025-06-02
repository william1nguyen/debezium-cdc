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

### Test

- Insert new data
  ```
  INSERT INTO demo_table (message) VALUES ('Message');
  ```