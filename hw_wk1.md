### Solutions for week 1

1. 
docker run -it --entrypoint=bash python:3.13-slim  
pip -V

2. db:5432

3. select count(*) from green_taxi_data where lpep_pickup_datetime >= '2025-11-01' and lpep_pickup_datetime < '2025-12-01'  and trip_distance <= 1.0 ;

4. select lpep_pickup_datetime, sum(trip_distance) as total_trip_dist  from green_taxi_data where trip_distance < 100.0 group by lpep_pickup_datetime order by sum(trip_distance) desc;

5. SELECT z.Zone AS pickup_zone,
       SUM(g.total_amount) AS total_amount_sum
FROM green_taxi_data g
JOIN zones_data z
  ON g.PULocationID = z.LocationID
WHERE g.lpep_pickup_datetime >= '2025-11-18'
  AND g.lpep_pickup_datetime < '2025-11-19'
GROUP BY z.Zone
ORDER BY total_amount_sum DESC
LIMIT 1;

6. SELECT dz.Zone AS dropoff_zone,
        (g.tip_amount) AS largest_tip
 FROM green_taxi_data g
 JOIN zones_data pz
   ON g.PULocationID = pz.LocationID
 JOIN zones_data dz
   ON g.DOLocationID = dz.LocationID
 WHERE pz.Zone = 'East Harlem North'
   AND g.lpep_pickup_datetime >= '2025-11-01'
   AND g.lpep_pickup_datetime < '2025-12-01'
 ORDER BY largest_tip DESC

 7. terraform init, terraform apply -auto-approve, terraform destroy