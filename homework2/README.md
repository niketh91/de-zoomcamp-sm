### Solutions for week 2

1. 128.3 MiB

2. green_tripdata_2020-04.csv

3. WITH rowcounts AS
(
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_01` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_02` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_03` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_04` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_05` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_06` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_07` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_08` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_09` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_10` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_11` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2020_12` GROUP BY filename
)

SELECT SUM(total_rows) FROM rowcounts

4. WITH rowcounts AS
(
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_01` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_02` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_03` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_04` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_05` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_06` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_07` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_08` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_09` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_10` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_11` GROUP BY filename
UNION ALL
SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.green_tripdata_2020_12` GROUP BY filename
)

SELECT SUM(total_rows) FROM rowcounts

5. SELECT filename, COUNT(unique_row_id) AS total_rows FROM `zoomcamphw2.yellow_tripdata_2021_03` GROUP BY filename

6. Add a timezone property set to America/New_York in the Schedule trigger configuration