# Answer 1.  20332093   

```sql
SELECT COUNT(*) FROM `xxx`;
```

# Answer 2. 0 MB for the External Table and 155.12 MB for the Materialized Table 


# Answer 3. BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.
```sql
SELECT PULocationID 
FROM `xxx`;

SELECT PULocationID, DOLocationID 
FROM `xxx`;
```


# Answer 4. 8,333
```sql
SELECT COUNT(*) AS zero_fare_count
FROM `xxx`
WHERE fare_amount = 0;

```

# Answer 5. Partition by tpep_dropoff_datetime and Cluster on VendorID
```sql
CREATE OR REPLACE TABLE `xxx`
PARTITION BY DATE(tpep_dropoff_datetime) 
CLUSTER BY VendorID 
AS
SELECT *
FROM `xxx`;
```

# Answer 6.  310.24 MB for non-partitioned table and 26.84 MB for the partitioned table
```sql
SELECT DISTINCT VendorID
FROM `xxx`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';


SELECT DISTINCT VendorID
FROM `xxx`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';
```

# Answer 7. GCP Bucket.

# Answer 8. False.
