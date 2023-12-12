
# Course Project
# Wildfire Analysis and Healthcare Impact - Del Rio
https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/blob/f43d29e0f87b7bb5598342dcc36ac79aff80f638/LICENSE\

# Goal of the project:
In recent years, the western United States has experienced an increasing frequency of wildfires, marking summers with billowing smoke that spans across vast regions. The causes behind this surge are many, compromising factors such as climate change, forestry policies, and growing awareness. The consequential impact of these wildland fires extends far beyond the immediate affected areas, affecting health, tourism, property, and various facets of society.

Del Rio, situated in Val Verde County, Texas, is a vibrant community that boasts a population of approximately 34,673 residents. Situated in the heart of the Lone Star State, this city experiences a Hot Semi-Arid climate, characterized by warm temperatures and relatively low precipitation. Del Rio's residents enjoy a unique blend of southwestern charm and Texan hospitality. The city's air quality is notably good, with an average Air Quality Index (AQI) of 40, indicating a relatively low level of air pollution. Del Rio's scenic landscapes and welcoming atmosphere make it a compelling destination for those seeking a taste of Texas living amidst a backdrop of arid beauty.
This analysis focuses on Del Rio, Texas, situated in Val Verde County, a region that has been immune to the encroaching consequences of wildfires. The motivation behind this exploration is rooted in the necessity to inform key decision-makers – including policymakers, city managers, and civic institutions – about the potential impact of wildfires on Del Rio. By delving into the correlations between wildfire-induced smoke exposure and various health outcomes, this study seeks to provide actionable insights that can guide the formulation of informed plans and strategies for mitigating future impacts.
Del Rio is situated on the border of Mexico and the USA, southwest in Texas. Most of the wildfires in Texas have been in the north eastern region of Texas.  Thus, based on these facts, some important research questions we would like to answer using this analysis are:
1.	Is Del Rio affected by smoke from wildfires in Texas?
2.	Does this increase the Smoke or AQI values for Del Rio?
3.	Does smoke from wildfires affect the health of residents of Del Rio?
   
The significance of this analysis lies in its potential to influence proactive decision-making. By understanding the historical patterns of wildfires, predicting future trends, and correlating these with health outcomes, we aspire to provide valuable insights that can shape public policies, environmental strategies, and healthcare interventions. Our ultimate goal is to contribute to the well-being and resilience of Del Rio and its residents in the face of an evolving environmental landscape.

**City for the analysis: Del Rio, Texas (County = Val Verde)**

# Licence: 
1.  [https://github.com/neelshah2302/data-512-course-project/blob/main/LICENSE](https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/blob/f43d29e0f87b7bb5598342dcc36ac79aff80f638/LICENSE)

# REST API Documentation and other sources: 
1. https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81
2. https://aqs.epa.gov/aqsweb/documents/data_api.html
3. https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf
4. https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81
5. https://healthdata.dshs.texas.gov/dashboard/births-and-deaths/deaths
6. https://www.dshs.texas.gov/vital-statistics-data
7. https://www.cancer-rates.com/tx/
8. https://seer.cancer.gov/ 

# Methodology:
<img width="872" alt="Screenshot 2023-12-11 at 9 12 23 PM" src="https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/assets/122260079/6eeb033a-bf63-44cc-94ec-d0c4d7d76992">

# Implementation

**1. Wildfire_Data_Extraction.ipynb -**

This notebook is used to extract the fires data from the wildfire dataset and to filter it based on certain conditions using the city assigned. The purpose of this code  to  find the fires which  are within 1250 miles of the assigned city - Del Rio, Texas
The data extraction code extracts data from the USGS Wildfire data and I found that there are 70861 fires which are  under 1250 miles from Del Rio based on distance.
The data is extracted based on 3 filters to create a smoke estimate at the end:
  1. The estimate only considers the last 60 years of wildland fires (1963-2023).
  2. The estimate only considers fires that are within 1250 miles of your assigned city.
  3. An annual fire season will run from May 1st through October 31st.

**2. AQI_Data_Extraction.ipynb-**

This notebook is used to extract AQI values from 1963 to 2023 around a specific city. I am using the reference code provided by the Prof for the data extraction which uses a US EPA API call to get the AQI information based on the fips for Del Rio, Texas. 
The AQI extraction will be done for each year and run from 1963 to 2023 for a specific fips number which we will obtain by finding the local AQI measurement sites around Del Rio, Texas

Del Rio is very remote and lies on the border of Mexico. Thus to get the monitoring stations, I had to increase the bounding boxes to a higher range. I found good 5 Monitoring stations around Del Rio, Texas, when I increased the bounding box scale to 250 Miles and finalized a fips number such that I have maximum AQI data.

**I finalized the monitoring station in Brewster, Texas with fips=48043 which started in 1988 to get as close AQI data as possible to 1963**

The code will extract daily AQI information for the monitoring station in Brewster Texas. I used a for loop to extract yearly data for these 60 years. The code will extract both gaseous and particulate AQI and store all of it as data frame extracted from dictionary format. I then combine the data frames and extract only the date, AQI, and pollutant type for each day.

**3. Data_Analysis_Prediction_and_Healthcare_Impact.ipynb-**

This Notebook is for analysis of the fire and AQI data extracted for Del Rio Texas and comparing certain results. The results/visualizations included are:
1. Produce a histogram showing the number of fires occurring every 50-mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.

Also, we are deploying a Predictive Model to predict the Smoke Estimate up to 2049 in the future. I have used Time Series forecasting model here: ARIMA for the prediction.

### Results:
The results from this analysis are produced in the form of 3 Visualizations:

  1. Histogram showing the number of fires occurring every 50 mile distance from your assigned city up to the max specified distance
     
     <img width="600" alt="Screenshot 2023-11-08 at 1 41 53 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/e0577165-f752-4b32-ba3e-8c0a5b23557e">


  2. Time series graph of total acres burned per year for the fires occurring in the specified distance from your city

     <img width="600" alt="Screenshot 2023-11-08 at 1 50 33 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/f8c940ec-2f03-4f15-995c-9bcca8c04b64">

  3. Time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.
     
     <img width="600" alt="Screenshot 2023-11-08 at 1 51 44 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/4ed16d5e-9023-464c-9969-93c12da8d9c4">


### Prediction:
Prediction of Smoking Estimate from 2024 to 2049 based on the historical data:

<img width="600" alt="Screenshot 2023-11-08 at 7 16 32 PM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/186ca414-cc71-4876-9312-412b9fe5e656">

### Healthcare Impact:

1.	Correlation Between Smoke Estimates and Deaths:
<img width="600" alt="image" src="https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/assets/122260079/1831a001-b46b-4132-bf99-cc15db2f96f9">
 
The analysis revealed a robust positive correlation of 64% between smoke estimates and overall deaths in Del Rio. Over the examined period (1970-2015), the number of deaths consistently increased in tandem with rising smoke estimates. This correlation suggests that smoke exposure from wildfires is a significant contributing factor to overall mortality in the region.

2.	Correlation Between Smoke Estimates and Cancer Mortality:
<img width="600" alt="image" src="https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/assets/122260079/4bd4e2da-88c5-463f-b32d-c0068b4417c3">

Contrary to the strong correlation observed for overall deaths, the relationship between smoke estimates and cancer mortality displayed a weaker correlation of 12%. While the number of cancer incidents and deaths increased (1995-2020 and 1990-2020, respectively), the correlation with smoke estimates was less pronounced. This suggests that other factors may play a more substantial role in cancer outcomes.

3.	Correlation Between Smoke Estimates and Infant/Fetal Mortality:
<img width="600" alt="image" src="https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/assets/122260079/448767eb-4568-475e-bfb1-73e42807c56d">

Unexpectedly, a negative correlation was identified for smoke estimates and infant/fetal mortality, with correlations of -53% and -25% respectively. The data indicates a decline in infant and fetal deaths, contrasting with the overall trend of increasing smoke estimates. This unexpected finding warrants further investigation into additional factors influencing infant and fetal mortality in the presence of wildfires.


# Data Description:

1.	Wildfire Data:

Column Name	Data Type	Description
OBJECTID	Integer	Unique identifier for each record in the dataset.
USGS_Assigned_ID	Numeric/String	Assigned identifier by the US Geological Survey (USGS) for the fire.
Assigned_Fire_Type	String	Type or classification of the assigned fire.
Fire_Year	Integer	The calendar year in which the fire occurred.
Fire_Polygon_Tier	String	Tier or level of classification for the fire polygon.
Fire_Attribute_Tiers	String	Tiers or levels of attributes associated with the fire.
GIS_Acres	Float	Area of the fire in acres according to the GIS data.
GIS_Hectares	Float	Area of the fire in hectares according to the GIS data.
Source_Datasets	String	List of datasets used as sources for fire information.
Listed_Fire_Types	String	Types of fires listed for the particular record.
Overlap_Within_1_or_2_Flag	String	Flag indicating overlap within 1 or 2 units.
Circleness_Scale	Float	Scale related to the circular shape of the fire.
Circle_Flag	String	Flag indicating whether the fire has a circular shape.
Exclude_From_Summary_Rasters	String	Flag indicating whether the fire should be excluded from summary rasters.
Shape_Length	Float	Length of the shape representation of the fire.
Shape_Area	Float	Area of the shape representation of the fire.
fire_lat	Float	Latitude of the fire location.
fire_lon	Float	Longitude of the fire location.
distance_from_del_rio	Float	Distance from Del Rio, a reference point, to the fire location.
smoke_estimate	Numeric	Estimate of smoke associated with the fire.

2.	AQI Data:

Column Name	Data Type	Description
date_local	Date	The local date for which air quality information is recorded.
pollutant_standard	String	The air quality pollutant standard being measured, such as PM2.5, PM10, Ozone, etc.
aqi	Integer	The Air Quality Index (AQI) value corresponding to the pollutant_standard for the given date_local. The AQI provides a numerical representation of the air quality level.

3.	Deaths by Race Data:

Column Name	Data Type	Description
Year	Integer	The calendar year in which the data was recorded.
All Races Total Deaths - Texas	Integer	The total number of deaths for all races in the state of Texas during the specified year.
All Races Total Deaths	Integer	The total number of deaths for all races across all regions during the specified year.
All Races Male Deaths	Integer	The total number of deaths for all races among males during the specified year.
All Races Female Deaths	Integer	The total number of deaths for all races among females during the specified year.
White Total Deaths	Integer	The total number of deaths among individuals identified as White during the specified year.
White Male Deaths	Integer	The total number of deaths among White males during the specified year.
White Female Deaths	Integer	The total number of deaths among White females during the specified year.
Black Total Deaths	Integer	The total number of deaths among individuals identified as Black during the specified year.
Black Male Deaths	Integer	The total number of deaths among Black males during the specified year.
Black Female Deaths	Integer	The total number of deaths among Black females during the specified year.
Hispanic* Total Deaths	Integer	The total number of deaths among individuals identified as Hispanic* during the specified year.
Hispanic* Male Deaths	Integer	The total number of deaths among Hispanic* males during the specified year.
Hispanic* Female Deaths	Integer	The total number of deaths among Hispanic* females during the specified year.
Other** Total Deaths	Integer	The total number of deaths among individuals identified as Other** during the specified year.
Other** Male Deaths	Integer	The total number of deaths among Other** males during the specified year.
Other** Female Deaths	Integer	The total number of deaths among Other** females during the specified year.


4.	Cancer Deaths Data:

Column Name	Data Type	Description
Year	Integer	The calendar year in which the data was recorded.
Population	Integer	The total number of individuals in a specified region or demographic during the year.
Cancer Deaths	Integer	The number of deaths attributed to cancer within the specified population and year.
Population affected	Integer	The count of individuals who have been diagnosed or affected by cancer in any form.
Cancer Incidents	Integer	The number of new cases of cancer reported or diagnosed within the specified population.

5.	Infants and Fetal Deaths Data:

Column Name	Data Type	Description
Year	Integer	The calendar year in which the data was recorded.
Infant Deaths	Integer	The number of deaths of infants (children below one year of age) during the year.
Infant Death Rate	Float	The rate of infant deaths per 1,000 live births during the specified year.
Fetal Deaths	Integer	The number of fetal deaths (stillbirths) during the specified year.
Fetal Death Ratio	Float	The ratio of fetal deaths to the total number of births during the specified year.

![image](https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/assets/122260079/bf9e6a6f-dbc8-43ad-b77a-475ff57dd9ba)



       

        



