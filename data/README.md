# Dataset

The dataset files are not included in this repository because they are large.

This project uses **March 2026 Yellow Taxi Trip Records** from the **New York City Taxi & Limousine Commission (NYC TLC)**. The data was downloaded from the official NYC TLC Trip Record Data page.

Dataset source:

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

---

## Dataset Files

The project workflow used three main Parquet files locally:

```text
data/
├── yellow_tripdata_2026-03.parquet
├── cleaned_taxi_data.parquet
└── final_taxi_data.parquet
```

---

## File Descriptions

### `yellow_tripdata_2026-03.parquet`

This is the original raw dataset downloaded from the NYC TLC Yellow Taxi Trip Records page.

It contains trip-level records for Yellow Taxi trips in **March 2026**. Each row represents one taxi trip.

Important columns include:

* `tpep_pickup_datetime`
* `tpep_dropoff_datetime`
* `PULocationID`
* `DOLocationID`
* `passenger_count`
* `trip_distance`
* `fare_amount`
* `tip_amount`
* `total_amount`
* `payment_type`

This file was used as the starting point for the big data analysis workflow.

---

### `cleaned_taxi_data.parquet`

This file contains the cleaned version of the raw taxi dataset.

The cleaning process included:

* Selecting only the columns relevant to demand, revenue, fare, location, and passenger behavior analysis.
* Removing rows with missing values in important columns.
* Removing trips with zero or negative trip distance.
* Removing trips with zero or negative fare or total amount.
* Keeping realistic passenger counts only.
* Removing invalid pickup or drop-off location IDs.
* Filtering extreme or unrealistic trip distance values.

This cleaned file was created to make the dataset more reliable for analysis and reduce the effect of invalid records on the final results.

---

### `final_taxi_data.parquet`

This file contains the final transformed dataset used for dashboarding and predictive modeling.

After cleaning, PySpark was used to create additional useful features, including:

* `pickup_hour`: the hour when the trip started.
* `pickup_day`: the day of the month.
* `pickup_date`: the pickup date.
* `trip_duration_minutes`: trip duration in minutes.
* `revenue_per_mile`: total revenue divided by trip distance.
* `payment_type_label`: readable payment type labels such as Credit card, Cash, Dispute, and No charge.

Additional filtering was applied to remove invalid transformed values, such as trips with unrealistic durations or invalid revenue per mile.

This final dataset was used for:

* Power BI dashboard visualizations.
* Demand analysis by time and location.
* Revenue analysis by pickup location and hour.
* Passenger behavior analysis.
* Payment method analysis.
* Spark ML Linear Regression modeling for fare prediction.

---

## Why the Dataset Is Not Uploaded

The original and processed Parquet files are large, so they are not uploaded to GitHub.

Instead, this repository includes:

* The notebook code.
* Dataset setup instructions.
* Dashboard screenshots.
* Documentation explaining the data pipeline.

---

## How to Reproduce the Dataset Locally

1. Download the March 2026 Yellow Taxi Trip Records file from the official NYC TLC page:

```text
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
```

2. Place the raw file inside a local `data/` folder.

3. Use the notebook:

```text
nyc_taxi_big_data_analytics.ipynb
```

4. Run the notebook cells to clean, transform, aggregate, and model the data.

5. If your local file paths are different, update the paths inside the notebook before running it.

---

## Important Note

The dataset files should remain local and should not be uploaded to GitHub.

The `.gitignore` file is configured to prevent large files such as `.parquet`, `.csv`, `.zip`, and `.pbix` files from being uploaded accidentally.
