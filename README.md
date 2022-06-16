# CS89 Project

## Yuchuan (Helen) Ma, Guhui Zhang

In this project, we aim to examine relationship between COVID cases and temperatures in the United States, with a primary focus on a selection of six states, including California, Texas, Florida, North Dakota, South Dakota, and Rhode Island.  
As of March 10, 2021, the former 3 states have the most significant number of confirmed cases, and the latter 3 have the most significant number of cases per million of population.  

## Data Source

### COVID-19 infected cases

- We rely on the Coronavirus Data in the United States dataset curated by The New York Times. The data tracks historical data of COVID infection by county since January 21, 2020.
- We also refer to the API of The COVID Tracking Project of The Guardian, which provides historical data on the number of infected cases by state and of the entire U.S.
- We scrape the daily COVID-19 updates provided by Worldometer to obtain the latest statistics (that is, of March 10, 2021) by state.

### Weather/temperature data

We utilize an API from the National Oceanic and Atmospheric Administration and access its Global Historical Climatology Network Daily (GHCND) dataset for the latter weather data. The dataset offers historical weather data on a weather station level that can be queried with FIPS code, a federal geographic information code for counties, and county-equivalent, if available.  

We collect the average temperature of each day (TAVG) in Fahrenheit. Since two weather stations observe two TAVG values for a given day and location, their mean is taken to represent the overall mean temperature.

### Method

1. We explore the correlations between the COVID spreading rates and the three ranges (3-day, 5-day, 10-day) of averaged temperatures for each county corresponding to a FIPS code within selected states. 
2. Pearson’s coefficient measures linear correlation, and Spearman’s rho and Kendall’s tau compare the data’s rank and thus capture the existence of a monotonic association between the spreading rates and average temperatures. 
3. To facilitate calculations, we add 0.0000001 to deal with zero-values in the spreading rates, i.e., when there are no increased cases during the given day, and further take the natural log to avoid floating-point errors.
4. We adopt K-Means clustering to cluster counties by their correlations between the spreading rates and averaged temperatures. Three Pearson’s coefficients, each for a temporal range, are the model features. The Elbow/Knee method is used to determine the number of clusters for the model with the lowest Sum of Squared Error (SSE).

## Files
1. The `weather_data` folder contains the weather (temperature) of the past year of six states.
2. In the `data` folder:
- `states.csv` has a list of states and their abbreviations
- `us_0310.csv` has the (cumulative) COVID data by state on March 10, 2021
- `us_daily.csv` has U.S. COVID data by date up until March 10, 2021
- `us_counties.csv` has U.S. COVID data by counties up until March 10, 2021
- `states_{state abbr}_daily_simple.csv` has COVID data of that state by counties up until March 10, 2021
- The original `.json` files used to generate the `.csv` files are also included
3. `noaa_datatypes.csv` has available observation data types (such as TAVG--average temperature) provided by NOAA.
4. `report.pdf` is a report of our project.
5. The `.ipynb` notebooks are named after their functionalities. We first retrieved the data, then explored them and finally modeled them.
