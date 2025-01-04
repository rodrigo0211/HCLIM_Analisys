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

### 1. Data Cleaning process carridd out in this research

0. Importing Files and Join them  
  0.1. Solving issue with pressure files  
  0.2. Splitting Date/Time column into Year and Month
2. Filling in Missing Elevation Values  
  1.1. Removing rows with any missing values in the variables.  
3. Check procedures  
  2.1. Same stations with multiple locations  
  2.2. Different stations with same LocationID  
  2.3. Same Stations with same LocationID (lat/Lon) and dif Elevation  
  2.4. Drop out all rows with year values before 1678  
  2.5. Aggregating  
  2.6. Detect and update non alphabetic letters in Station names  
4. FINDING BREAKINGPOINTS AND FILLING IN DATA (24 hours running time!!)  
  3.1. Double check breakpoints and fix if needed  s
5. STL (Seasonal-Trend decomposition)



