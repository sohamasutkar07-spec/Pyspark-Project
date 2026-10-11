# Brazilian E-Commerce Analytics with PySpark & Power BI

**Portfolio project | Python · PySpark · Power BI**

## Project overview

This project explores e-commerce order, customer, item, payment, product, seller, and review data from the Olist-style dataset files referenced in the notebooks. The notebook code demonstrates data loading, basic cleaning, timestamp conversion, joins, feature engineering, summary metrics, and CSV export for downstream dashboarding.

The Power BI report file and one dashboard screenshot are included in this repository.

## Analytical workflow in the notebooks

- Load CSV datasets for orders, customers, order items, payments, products, sellers, and reviews.
- Inspect schemas, sample records, and row counts.
- Remove duplicate rows from selected tables.
- Convert order and delivery fields to timestamps.
- Create delivery-delay and delivered-order indicator columns.
- Derive year and month fields for time-based analysis.
- Inspect order status, delivery delay, payment values, and basic summary statistics.
- Export a limited `fact_orders.csv` extract for use outside Spark.

## Repository contents

- [`Pyspark.ipynb`](Pyspark.ipynb) — notebook with loading, cleaning, joins, feature engineering, and summary queries.
- [`pyspark project.ipynb`](pyspark%20project.ipynb) — earlier / alternate notebook with overlapping steps.
- [`Project Pyspark.pbix`](Project%20Pyspark.pbix) — Power BI report file.
- [Dashboard screenshot](Screenshot%202026-03-27%20021014.png) — report visual reference.
- [`📊 Olist E.docx`](%F0%9F%93%8A%20Olist%20E.docx) — accompanying project document.

## Run the notebook

1. Install the packages used in the notebook, including `pyspark` and `pandas`.
2. Obtain the source CSV datasets referenced in the notebook. The raw data is not included in this repository.
3. Update the notebook's `base_path` variable to point to your local data directory. The current notebook contains an absolute Windows path that will not work on another machine unchanged.
4. Run the notebook cells in order.
5. If opening the PBIX file, check and update its source-data paths in Power BI Desktop, then refresh the report.

Example dependency installation:

```bash
pip install pyspark pandas
```

## Important validation notes

These are issues to review before treating the numeric outputs as business-ready:

- **Join grain and double counting:** order items, payments, and reviews may each contain multiple rows per order. Joining all of them at row level can multiply records and inflate sums or counts. For reliable KPIs, aggregate each one-to-many table to the intended grain before joining and reconcile totals to the source tables.
- **Missing review scores:** the current notebook replaces missing review scores with `0`. If calculating average ratings, treat missing ratings separately rather than assuming zero is a valid review score.
- **Local paths and exports:** the notebook uses a machine-specific Windows path and converts up to 100,000 rows to Pandas for CSV export. Update the path before execution and avoid collecting large datasets to the driver when the data exceeds local memory.
- **Reproducibility:** source CSV files are not stored here, and the notebook / PBIX has not been independently rerun end-to-end as part of this repository review.

## Skills demonstrated

- PySpark DataFrame operations
- CSV loading and schema inspection
- Deduplication and timestamp conversion
- Joins and feature engineering
- Basic aggregations and descriptive statistics
- Exporting analysis output for Power BI

## Limitations

This repository documents the workflow visible in the notebooks and files. Confirm source data, row-level grain, DAX measures, data model, and refresh behavior before using displayed totals as validated business results. The project is for portfolio and learning purposes.

## Author

Soham Asutkar
