### Answer 1. select * from myproject.raw_nyc_tripdata.ext_green_taxi

### Answer 2. Update the WHERE clause to pickup_datetime >= CURRENT_DATE - INTERVAL '{{ var("days_back", env_var("DAYS_BACK", "30")) }}' DAY

### Answer 3. dbt run --select models/staging/+

### Answer 4. Correct answers:
    Setting a value for DBT_BIGQUERY_TARGET_DATASET env var is mandatory, or it'll fail to compile
    When using core, it materializes in the dataset defined in DBT_BIGQUERY_TARGET_DATASET
    When using stg, it materializes in the dataset defined in DBT_BIGQUERY_STAGING_DATASET, or defaults to DBT_BIGQUERY_TARGET_DATASET
    When using staging, it materializes in the dataset defined in DBT_BIGQUERY_STAGING_DATASET, or defaults to DBT_BIGQUERY_TARGET_DATASET


# Answer 5. green: {best: 2020/Q2, worst: 2020/Q1}, yellow: {best: 2020/Q3, worst: 2020/Q4}

# Answer 6.  green: {p97: 40.0, p95: 33.0, p90: 24.5}, yellow: {p97: 31.5, p95: 25.5, p90: 19.0}

# Answer 7. LaGuardia Airport, Saint Albans, Howard Beach

