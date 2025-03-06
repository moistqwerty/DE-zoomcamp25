# Answer 1.  3.3.2
 
# Answer 2. 25 MB 
```python
# Import necessary libraries
from pyspark.sql import SparkSession

# Create a Spark session
spark = SparkSession.builder \
    .master("local[*]") \
    .appName("YellowTripData") \
    .getOrCreate()

df = spark.read.parquet("yellow_tripdata_2024-10.parquet")
df_repartitioned = df.repartition(4)
df_repartitioned.write.parquet("yellow_tripdata_repartitioned.parquet")

import os

parquet_dir = "yellow_tripdata_repartitioned.parquet"
parquet_size = sum(os.path.getsize(os.path.join(parquet_dir, f)) for f in os.listdir(parquet_dir))

parquet_size_mb = parquet_size / (1024 * 1024)
print(f"Total size of Parquet files: {parquet_size_mb:.2f} MB")

```

# Answer 3. 105,567
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, to_date


spark = SparkSession.builder \
    .master("local[*]") \
    .appName("YellowTaxiTripCount") \
    .getOrCreate()


df = spark.read.parquet("yellow_tripdata_2024-10.parquet")

df_filtered = df.filter(to_date(col("pickup_datetime")) == "2024-10-15")


trip_count = df_filtered.count()

print(f"Number of trips on October 15th, 2024: {trip_count}")
```


# Answer 4. 142
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, unix_timestamp

spark = SparkSession.builder \
    .master("local[*]") \
    .appName("LongestTaxiTrip") \
    .getOrCreate()


df = spark.read.parquet("yellow_tripdata_2024-10.parquet")


df_with_duration = df.withColumn(
    "duration_seconds", 
    (unix_timestamp("dropoff_datetime") - unix_timestamp("pickup_datetime"))
)


df_with_duration = df_with_duration.withColumn(
    "duration_hours", col("duration_seconds") / 3600
)


max_duration = df_with_duration.agg({"duration_hours": "max"}).collect()[0][0]

print(f"Longest trip duration: {max_duration:.2f} hours")
```

# Answer 5. 4040


# Answer 6. Governor's Island/Ellis Island/Liberty Island
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

spark = SparkSession.builder \
    .master("local[*]") \
    .appName("LeastFrequentPickupZone") \
    .getOrCreate()

zone_df = spark.read.option("header", "true").csv("taxi_zone_lookup.csv")

zone_df.createOrReplaceTempView("zone_lookup")

df = spark.read.parquet("yellow_tripdata_2024-10.parquet")

df_with_zones = df.join(
    spark.sql("SELECT * FROM zone_lookup"), 
    df.PULocationID == zone_df.LocationID, 
    "inner"
)

zone_pickup_counts = df_with_zones.groupBy("Zone").count().orderBy("count")

least_frequent_zone = zone_pickup_counts.first()["Zone"]

print(f"Least frequent pickup location zone: {least_frequent_zone}")
```
