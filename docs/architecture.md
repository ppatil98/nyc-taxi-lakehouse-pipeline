# Pipeline Plan

## Source
NYC TLC Yellow Taxi trips (January 2025, Parquet) and Taxi Zone Lookup (CSV),
uploaded to /Volumes/workspace/bronze/raw_files.

## Bronze (raw, unchanged)
- Load the Parquet file as-is into bronze.yellow_trips_raw
- Add ingestion_timestamp and source_file columns
- Load the zone lookup CSV into bronze.taxi_zones_raw

## Silver (cleaned)
- Cast data types
- Remove rows with null pickup or dropoff times
- Remove trips with negative fare or distance
- Remove trips where dropoff is before pickup
- Deduplicate

## Gold (star schema)
- fact_trips
- dim_zone
- dim_date
- dim_payment_type
- agg_daily_revenue_by_zone (for the dashboard)

## Data quality checks
- Row counts per layer
- Null checks on key columns
- Rejected-row count in silver
