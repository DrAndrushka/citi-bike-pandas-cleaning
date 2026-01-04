# Citi Bike (JC) — Pandas Data Cleaning (2016)

This mini-project cleans and standardizes Citi Bike trip CSV data using **pandas**, producing an analysis-ready dataset plus explicit flags for missing and suspicious records.

## What I did
- Loaded and concatenated multiple tripdata CSV files into a single DataFrame
- Renamed columns to a consistent `snake_case` schema
- Converted `start_time` / `stop_time` to `datetime64[ns]`
- Computed `trip_duration` as a `timedelta64[ns]` (`stop_time - start_time`)
- Cleaned categorical fields:
  - mapped `gender` codes (1 → `male`, 2 → `female`, 0 → `NaN`)
- Added quality flags for easier analysis:
  - `missing_user_type`, `missing_birth_year`, `missing_gender`
  - `has_missing` (any missing demographic field)
  - `age` (ride year − `birth_year`)
  - `has_bad` (implausible / suspicious values such as non-positive duration, placeholder birth years, or extreme durations)
- Created an analysis-ready subset:
  - `no_missing = bikes[(~bikes.has_missing) & (~bikes.has_bad)]`

## Data
Raw tripdata CSVs are not included in this repo (file size).

Download the starter dataset here:
https://static-assets.codecademy.com/Paths/data-engineering-career-path/bike-rental-data-management/bike-rental-starter-kit.zip

Unzip it and place the CSV files into a local `data/` folder.

Expected filename pattern:
```
data/JC-*-citibike-tripdata.csv
```

Note: Dataset is provided by Codecademy as part of their Data Engineering path.

## How to run
1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Open and run the notebook:
- `bike-rental.ipynb`

## Output
- `bikes`: cleaned dataset with derived columns and flags
- `no_missing`: filtered dataset excluding missing and flagged “bad” records

## Tech
- Python
- pandas
- numpy
