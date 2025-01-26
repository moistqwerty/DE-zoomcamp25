Question 1. Version of pip:

docker run -it --entrypoint bash python:3.12.8
pip --version
pip 24.3.1

Question 2. Understanding Docker networking and docker-compose

db:5433

Question 3. Trip Segmentation Count

SELECT
    COUNT(*) AS trip_count,
    CASE
        WHEN trip_distance <= 1 THEN 'Up to 1 mile'
        WHEN trip_distance > 1 AND trip_distance <= 3 THEN 'Between 1 and 3 miles'
        WHEN trip_distance > 3 AND trip_distance <= 7 THEN 'Between 3 and 7 miles'
        WHEN trip_distance > 7 AND trip_distance <= 10 THEN 'Between 7 and 10 miles'
        ELSE 'Over 10 miles'
    END AS distance_range
FROM green_taxi
WHERE lpep_pickup_datetime BETWEEN '2019-10-01' AND '2019-11-01'
GROUP BY distance_range
ORDER BY trip_count DESC;

"trip_count"	"distance_range"
198995	"Between 1 and 3 miles"
109642	"Between 3 and 7 miles"
104830	"Up to 1 mile"
35201	"Over 10 miles"
27686	"Between 7 and 10 miles"

Question 4. Longest trip for each day

"""
SELECT 
    DATE(lpep_pickup_datetime) AS pickup_day,
    MAX(trip_distance) AS longest_trip_distance
FROM green_taxi
WHERE DATE(lpep_pickup_datetime) IN ('2019-10-11', '2019-10-24', '2019-10-26', '2019-10-31')
GROUP BY pickup_day
ORDER BY pickup_day;
"""
"""
"pickup_day"	"longest_trip_distance"
"2019-10-11"	95.78
"2019-10-24"	90.75
"2019-10-26"	91.56
"2019-10-31"	515.89
"""

Question 5. Three biggest pickup zones

SELECT 
    z."Zone" AS pickup_location,
    SUM(g.total_amount) AS total_revenue
FROM green_taxi g
JOIN zones z
    ON g."PULocationID" = z."LocationID"
WHERE DATE(g.lpep_pickup_datetime) = '2019-10-18'
GROUP BY z."Zone"
HAVING SUM(g.total_amount) > 13000
ORDER BY total_revenue DESC;

"pickup_location"	"total_revenue"
"East Harlem North"	18686.680000000077
"East Harlem South"	16797.260000000068
"Morningside Heights"	13029.79000000004

Question 6. Largest tip

SELECT 
    dz."Zone" AS dropoff_zone,
    MAX(g.tip_amount) AS max_tip
FROM green_taxi g
JOIN zones pz
    ON g."PULocationID" = pz."LocationID"
JOIN zones dz
    ON g."DOLocationID" = dz."LocationID"
WHERE 
    pz."Zone" = 'East Harlem North'
    AND g.lpep_pickup_datetime BETWEEN '2019-10-01' AND '2019-11-01'
GROUP BY dz."Zone"
ORDER BY max_tip DESC
LIMIT 1;

Answer: JFK

Question 7. Terraform Workflow

terraform init, terraform apply -auto-approve, terraform destroy
