# Answer 1. 128.3 MB  

# Answer 2. green_tripdata_2020-04.csv  

# Answer 3. 24,648,499
```sql
SELECT COUNT(*) AS total_rows
FROM `vast-watch-448404-d4.zoomcamp.yellow_tripdata`
WHERE EXTRACT(YEAR FROM tpep_pickup_datetime) = 2020;
```

# Answer 4. 1,734,051
```sql
SELECT COUNT(*) AS total_rows
FROM `vast-watch-448404-d4.zoomcamp.green_tripdata`
WHERE EXTRACT(YEAR FROM lpep_pickup_datetime) = 2020;
```

# Answer 5. 1,925,152
```sql
SELECT COUNT(*) AS total_rows
FROM `vast-watch-448404-d4.zoomcamp.yellow_tripdata_2021_03`;
```


# Answer 6. Add a timezone property set to America/New_York in the Schedule trigger configuration
