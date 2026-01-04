# Citi Bike (JC) — Pandas Data Cleaning (2016)

This mini-project cleans and standardizes Citi Bike trip CSV data using **pandas**, producing an analysis-ready dataset plus explicit flags for **missing** and **suspicious** records.

---

## Dataset

Starter kit (Codecademy):  
https://static-assets.codecademy.com/Paths/data-engineering-career-path/bike-rental-data-management/bike-rental-starter-kit.zip

> Note: The large raw CSV files are **not committed** to this repo (see `.gitignore`).  
> Download them from the link above and place them into `data/`.

---

## What I did

- Loaded and concatenated multiple tripdata CSV files into a single DataFrame
- Renamed columns to a consistent `snake_case` schema
- Converted `start_time` / `stop_time` to `datetime64[ns]`
- Computed `trip_duration` as `timedelta64[ns]` (`stop_time - start_time`)
- Cleaned categorical fields:
  - mapped gender codes (`1 → male`, `2 → female`, `0 → NaN`)
- Added quality flags for easier analysis:
  - `missing_user_type`, `missing_birth_year`, `missing_gender`
  - `has_missing` (any missing demographic field)
  - `age` (ride year − `birth_year`)
  - `has_bad` (suspicious values such as non-positive duration, placeholder birth years like `<= 1900`, and other detected outliers)
- Created an analysis-ready subset excluding flagged rows:
  - `no_missing = bikes[(~bikes.has_missing) & (~bikes.has_bad)]`

---

## Repo contents

- `bike-rental.ipynb` — notebook with the cleaning steps + checks
- `README.md` — this file
- `requirements.txt` — minimal dependencies
- `.gitignore` — prevents committing large raw data files

---

## How to run

### 1) Install dependencies
```bash
pip install -r requirements.txt
```

### 2) Get the data
Download the starter kit ZIP (link above), unzip it, and place the CSVs into:
```
data/
```

### 3) Run the notebook
Open and run:
- `bike-rental.ipynb`

---

## Output

The notebook produces:
- a cleaned DataFrame (`bikes`) with added flags/features
- an analysis-ready subset (`no_missing`) for downstream analytics

(Export to CSV is optional and intentionally not committed due to file size.)
