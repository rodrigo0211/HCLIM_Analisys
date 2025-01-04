# HCLIM Analisys
## Data Clenaing, Analisys and Visualization of HCLIM dataset

### 1. HCLIM info

Paper can be found in:
- SMHI (Swedish Meteorological and Hydrological Institute) -> [download]( https://www.smhi.se/en/research/research-departments/climate-research-at-the-rossby-centre/harmonie-1.135580 "download paper from SMHI")
- *nature.com* -> [download]( https://www.nature.com/articles/s41597-022-01919-w "download paper from nature.com") 

Taking advantage from the Global Early Instrumental Monthly Meteorological Multivariable Database, the HCLIM (Historical Climate Dataset) provides a full compilation of historical climate records dating back before 1890 and offers a unique opportunity to apply advanced geostatistical methods to predict climate variables at a specific location, at a specific date.

HCLIM provide with public dataset concerning monthly values for **TEMPERATURE**, **PRECIPITATION**, **WET DAYS** and **PREASSURE**. The collection totals 12,452 records (meteorological time series with one variable at one location) in 118 countries and more than 10 million rows.

![image](https://github.com/user-attachments/assets/9726d106-5c37-4046-a341-6f12c43d1987)

Below are the location of the 12,000 stations for the precipitations file:

![image](https://github.com/user-attachments/assets/26b51324-1f6d-44f0-ba03-4c1334b6a4f4)

### 1. Data Cleaning process carried out in this research  

**0. Importing Files and Join them**  
&nbsp;&nbsp;&nbsp;&nbsp;**0.1. Solving issue with pressure files**  
&nbsp;&nbsp;&nbsp;&nbsp;**0.2. Splitting Date/Time column into Year and Month**  

**1. Filling in Missing Elevation Values**  
The Open-Elevation API is a free, open-source service that provides elevation data for any point on Earth. It acts as an alternative to commercial elevation services like the Google Elevation API, aiming to democratize access to topographic data.  
The service relies on publicly available elevation datasets, such as SRTM (Shuttle Radar Topography Mission) data, and allows users to query elevation information by providing latitude and longitude values through a simple HTTP API interface.  
Technically, the Open-Elevation API supports both GET and POST HTTP methods for querying elevation data.  
Users can request elevation information for multiple points in a single request by submitting a list of latitude and longitude pairs. The service then returns a JSON response containing the elevation in meters for each requested point. For bulk queries, the POST method is recommended, allowing users to submit their queries in the body of the request in JSON format.  
ElevationAdded column is added for traceability purposes  

&nbsp;&nbsp;&nbsp;&nbsp;**1.1. Removing rows with any missing values in the variables.**  

ASUMPTION: df_PoPoPoPo and df_PPPP are small datasets and we are not working with them  

**2. Check procedures**  
&nbsp;&nbsp;&nbsp;&nbsp;**2.1. Same stations with multiple locations**  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Col LocationID is added as a combination of Lat/Lon  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - If the locationID are different, then add suffix (2..) to the name  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Col StationUpdated added for traceability reasons  

&nbsp;&nbsp;&nbsp;&nbsp;**2.2. Different stations with same LocationID**  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - There are Statsions that share LocationID (Lat, Long) values (same values)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - To prevent from mistakes in future calculations, grouping, 0.06 is added to the Latitude value  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - unique_stations_per_location stores the LocationIDs affected and Stations per LocationID  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Also a new column UpdatedLatLong is added for traceability reasons  

&nbsp;&nbsp;&nbsp;&nbsp;**2.3. Same Stations with same LocationID (lat/Lon) and dif Elevation**  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - The most frequent Elevation is selected and all rows are updated with that value.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - A new column ElevationUpdated is added for traceability purposes

&nbsp;&nbsp;&nbsp;&nbsp;**2.4. Drop out all rows with year values before 1678**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - the lower-limit to work with Dates in "pandas" df is year 1678

&nbsp;&nbsp;&nbsp;&nbsp;**2.5. Aggregating**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - There are rows with same station, locationID and Date/Time. Only one must remain. The value of the variable is averaged  

&nbsp;&nbsp;&nbsp;&nbsp;**2.6. Detect and update non-alphabetic letters in Station names**  

**3. Finding breakpoints and filling data (24 hours running time in my laptop!!)**  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CRITERIA:  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Check how many rows with Month value from every Year for a certain locationID exists. For the missing rows of each Month, add the corresponding rows using the average WetDays/Precipitation/Temp value of the first existing previous month/year and next month/year  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Check if for each group there is any year missing. For every year missing, create the corresponding 12 rows (one per each month) with the values for WetDays (and the rest of the variables) following the method forward or backward search implemented already  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Add a column "rowAdded" with 1 for the new rows added, and 0 for the rest  

&nbsp;&nbsp;&nbsp;&nbsp;**3.1. Double check breakpoints and fix if needed**  

**4. STL (Seasonal-Trend decomposition)**  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - using LOESS (Locally Estimated Scatterplot Smoothing)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - https://www.statsmodels.org/devel/examples/notebooks/generated/stl_decomposition.html  

![image](https://github.com/user-attachments/assets/05d97ce5-1516-4c09-8347-4063183727f6)

(*) SRD: Seasonally Removed Data

### 2.  Finding breakpoints and filling data explanation in detail

![image](https://github.com/user-attachments/assets/8dcf7d6f-3a1e-4233-8cb7-21321946417a)

### 3. Future Work: TIME SERIES ANALISYS - SPATIO TEMPORAL ANALISYS

- The first attempt is to perform a pure time forecasting using **ARIMA**  
- Then, perform a vainilla **SPATIAL KRIGING**  
- Take advantage of the updated **SPATIO-TEMPORAL KRIGING**  
Other spatio-temporal models to be evaluated:  
&nbsp;&nbsp;&nbsp;&nbsp;✓ KRK (Fixed Rank kriging)  
&nbsp;&nbsp;&nbsp;&nbsp;✓ Empirical Orthogonal Functions (EOFs)  
&nbsp;&nbsp;&nbsp;&nbsp;✓ Cokriging  
&nbsp;&nbsp;&nbsp;&nbsp;✓ Bayesian Hierarchical Models  
&nbsp;&nbsp;&nbsp;&nbsp;✓ Generalized Additive Models (GAMs) in Space and Time  





