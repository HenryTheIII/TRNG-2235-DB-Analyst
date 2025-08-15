# Air Quality Index (AQI) Trend Analysis – USA (2020–2024)

## Project Objective

To analyze and visualize trends in air quality across the United States over the last five years (2020–2024), using EPA-published datasets. The project aims to:

* Understand national, state, and regional air quality patterns.
* Compare metrics across counties and CBSAs.
* Analyze pollutant-specific behavior and their annual variations.
* Compare urban (CBSA) and rural (non-CBSA counties) air quality metrics.

## Datasets Required

**Source:** U.S. Environmental Protection Agency (EPA) - [AirData Download](https://aqs.epa.gov/aqsweb/airdata/download_files.html)

- `AQI by CBSA`
- `AQI by County`

### 1. Annual AQI by County

* File: `annual_aqi_by_county_<year>`
* Granularity: County-level
* Fields: State, County, Year, AQI Days, Good Days, Moderate Days, Unhealthy Days (various levels), Hazardous days, Max AQI, 90th Percentile AQI,	Median AQI, Days per pollutant (CO, NO2, Ozone, PM2.5, PM10)

### 2. Annual AQI by CBSA (Core-Based Statistical Area)

* File: `annual_aqi_by_cbsa_<year>.csv`
* Granularity: Urban/Metropolitan-level
* Fields: CBSA Name (e.g., "Chicago-Naperville-Elgin, IL-IN-WI"), State, AQI Days, Good Days, Moderate Days, Unhealthy Days (various levels), Hazardous Days, Max AQI, 90th Percentile AQI,	Median AQI, Days per pollutant (CO, NO2, Ozone, PM2.5, PM10)


## Data Preparation

1. **Load and Merge Data**:

   * Load 5 years of data separately for County and CBSA.
   * Combine each into two unified DataFrames:

     * `aqi_county_df`
     * `aqi_cbsa_df`

2. **Preprocessing Steps**:

   * Normalize column names and text values (e.g., counties, CBSA names).
   * Standardize year as integer.
   * Clean CBSA names and extract base CBSA and state if needed.
   * Add FIPS codes for counties

## Core Analyses

### A. National Trends

* Year-over-year trend of "Good" vs "Unhealthy" days.
* Annual Max AQI, 90th Percentile AQI, and Median AQI comparison.
* Nation-level pollutant day breakdown (CO, NO2, Ozone, PM2.5, PM10).

<i> <b>Note</b>: Represents county-level monitoring coverage, not population-weighted national exposure</i>

### B. County-Level Analysis

* Top 10 counties with most "Unhealthy for Sensitive Groups", "Unhealthy" and "Hazardous" days.
* State-wise comparison of all its counties.
* Pollutant-specific distribution by county and year.

### C. CBSA-Level Analysis

* Top 10 CBSAs with most "Unhealthy for Sensitive Groups", "Unhealthy" and "Hazardous" days.
* Trend analysis across CBSAs.
* Compare AQI trends between Metropolitan and Micropolitan areas. (reference [CBSAs Code Table](https://aqs.epa.gov/aqsweb/documents/codetables/cbsas.csv))
* Pollutant distribution across zones.

### D. Combined & Comparative Analysis - Optional

- [cbsa - county](https://www2.census.gov/programs-surveys/metro-micro/geographies/reference-files/2023/delineation-files/list1_2023.xlsx)

1. **Urban (CBSA) vs Rural (County)**

   * Tag counties not mapped to CBSAs as rural.
   * Use CBSA tags to classify urban zones.
   * Compare annual AQI trends between rural counties and urban CBSAs.

2. **CBSA and County Overlap**

   * For each state, extract and match CBSA base name and associated counties (e.g., LA County vs LA CBSA).
   * Key metrics to compare:
    - Median AQI (represents typical day-to-day air quality)
    - 90th Percentile AQI (indicates severity of worst pollution days, excluding rare extremes)
    - Max AQI
    - Share of Good vs Unhealthy days
    - Dominant pollutants and their frequency

3. **Regional Pollutant Behavior**

   * Compare top pollutants across counties vs CBSAs.
   * Identify regional shifts in pollutant dominance.

<i><b>Note:</b><i>
  - <i>County-to-CBSA matching across 5 years may require optimization</i>
  - <i>Consider performance implications of large joins</i>
  - <i>Plan for efficient data storage and retrieval strategies</i>

## Visualizations

* **Line Charts**: 5-year AQI category trend by region.
* **Stacked Bar Charts**: Yearly breakdown of AQI categories.
* **Heatmaps(Optional) or Scatter Plots with color coding**: Max AQI values across counties/CBSAs.
* **Side-by-Side Bar Graphs**: County vs CBSA comparison for top metros.
* **Pie Charts**: Contribution of pollutants to Unhealthy days.
* **Boxplots**: Distribution of AQI values across counties/CBSAs.

## Deliverables

* Cleaned, preprocessed datasets (Delta/Parquet) 
* Databricks Notebook or script for:

  * Preprocessing
  * Visualizations
  * Summary statistics

* Final report with:
  * Key findings
  * Visuals with captions
  * Observations at national, regional, and urban vs rural levels

* Interactive dashboard with filters

## Optional Extensions

* Forecast AQI for 2025

## Notes

* Use only EPA-published data.
* Maintain consistency in AQI scale and category naming conventions.
* Encourage exploratory thinking for optional analysis beyond the core scope.
