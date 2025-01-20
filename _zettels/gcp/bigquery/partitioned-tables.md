---
date: 2025-01-17
layout: zettel
category: show
tags:
  - gcp
  - bigquery
  - article
title: the case for (date) partitioned table
article-name: Official Docs
link: https://www.cloudskillsboost.google/games/5837/labs/37167
---
- Query 1: 5 rows returned and 1.74 GB processed
```
SELECT DISTINCT
  fullVisitorId,
  date,
  city,
  pageTitle
FROM `data-to-insights.ecommerce.all_sessions_raw`
WHERE date = '20170708'
LIMIT 5
```

- Query 2: 0 Rows returned still 1.74 GB processed
```
SELECT DISTINCT
  fullVisitorId,
  date,
  city,
  pageTitle
FROM `data-to-insights.ecommerce.all_sessions_raw`
WHERE date = '20180708'
LIMIT 5
```

- Why?
	- Before the query runs, the query engine does not know whether 2018 data exists to satisfy the WHERE clause condition and it needs to scan through all records in a non-partitioned table.
- Scanning the entire dataset to apply a WHERE condition is inefficient, particularly when focusing on records from specific timeframes, such as the last year, last 7 days, or last month. To optimize this process, it is advisable to use a date-partitioned table. This approach enables the system to skip irrelevant partitions, streamlining the querying process and improving performance.
- Creating Date Partitioned table
```
CREATE OR REPLACE TABLE ecommerce.partition_by_day
PARTITION BY date_formatted
OPTIONS(
description="a table partitioned by date"
) AS
SELECT DISTINCT
PARSE_DATE("%Y%m%d", date) AS date_formatted,
fullvisitorId
FROM `data-to-insights.ecommerce.all_sessions_raw`
```

- Auto Expiring:
	- Auto-expiring partitioned tables help meet data privacy regulations and reduce unnecessary storage costs. 
	- By assigning expiration dates to partitions, you can create a rolling window of data that automatically deletes partitions once they are no longer needed.
```
 CREATE OR REPLACE TABLE ecommerce.days_with_rain
 PARTITION BY date
 OPTIONS (
   partition_expiration_days=60,
   description="weather stations with precipitation, partitioned by day"
 ) AS
 SELECT
   DATE(CAST(year AS INT64), CAST(mo AS INT64), CAST(da AS INT64)) AS date,
   (SELECT ANY_VALUE(name) FROM `bigquery-public-data.noaa_gsod.stations` AS stations
    WHERE stations.usaf = stn) AS station_name,  -- Stations may have multiple names
   prcp
 FROM `bigquery-public-data.noaa_gsod.gsod*` AS weather
 WHERE prcp < 99.9  -- Filter unknown values
   AND prcp > 0      -- Filter
   AND _TABLE_SUFFIX >= '2018'
```
