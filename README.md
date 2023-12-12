
# Course Project
# Wildfire Analysis and Healthcare Impact - Del Rio

[![GitHub license](https://img.shields.io/github/license/neelshah2302/data-512-wildfire-analysis-delrio)](https://github.com/neelshah2302/data-512-wildfire-analysis-delrio/blob/f43d29e0f87b7bb5598342dcc36ac79aff80f638/LICENSE)

# Part 1 - Common Analysis

# Goal of the project:
More and more frequently summers in the western US have been characterized by wildfires with smoke billowing across multiple western states. There are many proposed causes for this: climate change, US Forestry policy, and growing awareness, just to name a few. Regardless of the cause, the impact of wildland fires is widespread. There is a growing body of work pointing to the negative impacts of smoke on health, tourism, property, and other aspects of society.

The course project will require that we analyze wildfire impacts on a specific city in the US. The end goal is to be able to inform policymakers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires.

**City assigned to me for the analysis: Del Rio, Texas (County = Val Verde)**

For the Part 1 Common Analysis, we will perform the following High-level steps:
1. Wildfire Data extraction for a specific city
2. AQI Data Extraction for a specific city
3. Predictive Model Deployment
4. Data Analysis

Step 1 and Step 2 correspond to Data extraction of Wildfire data by downloading the data and processing from https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81 and web scrapping the AQI data using US EPA API respectively.

For step 3, we need to develop a predictive model based on the fire data and smoke estimate for our assigned city. The model should predict smoke estimates for every year for the next 25 years (i.e., 2024-2049).

For step 4, We will perform an analysis of smoke estimates defined by us for the city and the AQI extracted from monitoring stations near the city. The analysis will consist of visualizations answering the following:
1. Produce a histogram showing the number of fires occurring every 50-mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.

In the end, we need to write a short reflection on the project that focuses on both the findings from this analysis and the collaborative aspect of the assignment.

# Licence: 
1.  https://github.com/neelshah2302/data-512-course-project/blob/main/LICENSE

# REST API Documentation and other sources: 
1. [https://www.mediawiki.org/wiki/API:Info](https://aqs.epa.gov/aqsweb/documents/data_api.html)
2. https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf
3. https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81

# Implementation:

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

**3. Data_Analysis_and_Prediction.ipynb-**

This Notebook is for analysis of the fire and AQI data extracted for Del Rio Texas and comparing certain results. The results/visualizations included are:
1. Produce a histogram showing the number of fires occurring every 50-mile distance from your assigned city up to the max specified distance.
2. Produce a time series graph of total acres burned per year for the fires occurring in the specified distance from your city.
3. Produce a time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.

Also, we are deploying a Predictive Model to predict the Smoke Estimate up to 2049 in the future. I have used Time Series forecasting model here: ARIMA for the prediction.

### Results:
The results from this analysis are produced in the form of 3 Visualizations:

  1. Histogram showing the number of fires occurring every 50 mile distance from your assigned city up to the max specified distance
     
     <img width="866" alt="Screenshot 2023-11-08 at 1 41 53 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/e0577165-f752-4b32-ba3e-8c0a5b23557e">


  2. Time series graph of total acres burned per year for the fires occurring in the specified distance from your city

     <img width="844" alt="Screenshot 2023-11-08 at 1 50 33 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/f8c940ec-2f03-4f15-995c-9bcca8c04b64">

  3. Time series graph containing your fire smoke estimate for your city and the AQI estimate for your city.
     
     <img width="842" alt="Screenshot 2023-11-08 at 1 51 44 AM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/4ed16d5e-9023-464c-9969-93c12da8d9c4">


### Prediction:
Prediction of Smoking Estimate from 2024 to 2049 based on the historical data:

<img width="856" alt="Screenshot 2023-11-08 at 7 16 32 PM" src="https://github.com/neelshah2302/data-512-course-project/assets/122260079/186ca414-cc71-4876-9312-412b9fe5e656">


       

        



