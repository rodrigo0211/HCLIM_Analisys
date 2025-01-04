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
&nbsp;&nbsp;&nbsp;&nbsp;**2.3. Same Stations with same LocationID (lat/Lon) and dif Elevation**  
&nbsp;&nbsp;&nbsp;&nbsp;**2.4. Drop out all rows with year values before 1678**  
&nbsp;&nbsp;&nbsp;&nbsp;**2.5. Aggregating**  
&nbsp;&nbsp;&nbsp;&nbsp;**2.6. Detect and update non-alphabetic letters in Station names**  

**3. FINDING BREAKINGPOINTS AND FILLING IN DATA (24 hours running time!!)**  
&nbsp;&nbsp;&nbsp;&nbsp;**3.1. Double check breakpoints and fix if needed**  

**4. STL (Seasonal-Trend decomposition)**  






