# NYPD Complaint Classification
Stat 426 Final Project

## Introduction
Crime across the United States is a constant part of life. However, in the past year and a half there has been a rise in understanding crime as it has to do with racial discrimination and other factors. Often, certain areas are over policed or certain crimes are dealt with more harshly based on factors that are not fully understood. While we cannot fully understand all factors that play apart in crime our project is trying to explore what affects the severity of a crime.

Using data found from historic New York Police Department (NYPD) [complaint report](https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i ) we are attempting to classify the severity of a crime, or offense level, based on features such as age, race, location, time of day, and sex for the NYPD.  The data used includes all valid felony, misdemeanor, and violation crimes reported to the NYPD from 2006 to the end 2019. There are over 7 million different complaints but for this project we will only look at the last 50,000 complaints to ensure our machines can handle the data.

We will use different classification machine learning models to learn from our data and then predict the offense level of a Misdemeanor, Felony, or Violation and see which features are the most significant in determining the severity. We think that age, race, and time of day might be factors that help predict severity more significantly than other features.

We will be using the following steps and have used several juypter notebooks in this repository to break up our work that can be easily followed:
1. Collecting and Cleaning the Data- found in  [DataCleaning.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/DataCleaning.ipynb)
2. Exploring the Data - found in [ExploratoryDataAnalysis.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/ExploratoryDataAnalysis%20.ipynb)
3. Model Prediction and Evaluation - found in [Modelipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Model.ipynb)

## Data Collection and Cleaning
As previously mentioned we used NYPD complaint data. We obtained our data using the Socrata API and got 50,000 of the results. From the inital read in from the API we have 40 different features for our data. Many of the features are redundant information, for example a written name of the station number and anoher feature is a numerical number for the same staion number, and we decided to drop them from the data. Additionally we dropped any feature that would inherintly tell us the severity of the crime. 

After dropping columns we turned our dates to only have the Month (1-12) and Time of day (4 different quarters). Aditionally we turned the houinsing development names into a binary 1 or 0 to indicate if the complaint took place in a housing development. We standardized all entires that were labled as 'UNKNOWN' or 'U' to NaN. Lastly we had to change our features that have ages to not include negative ages or values that were unreasonably high. 

Our final data set after all cleaning has the following 17 features:

|Variable|Description|
|:-|:-|
|month|Month (1-12) of occurrence for the reported event|
|time_of_day|Time of occurrence for the reported event (1= morning: 5 AM - Noon, 2= afternoon: Noon - 6 PM, 3= evening: 6 PM - 10 PM, 4= night: 10 PM - 5 AM|
|precinct|  The precinct in which the incident occurred |                   
|crime_completed|Indicator of whether crime was successfully completed or attempted, but failed or was interrupted prematurely |
|offense_level   |     Level of offense: felony, misdemeanor, violation|     
|borough_nam        |       The name of the borough in which the incident occurred|
|premises   |      Specific description of premises; grocery store, residence, street, etc.|
|jurisdiction_code       |       Description of the jurisdiction code|
|latitude    |Midblock Latitude coordinate for Global Coordinate System, WGS 1984, decimal degrees (EPSG 4326)| 
|longitude   |Midblock Longitude coordinate for Global Coordinate System, WGS 1984, decimal degrees (EPSG 4326)
|vic_age_group       |  Victim’s Age Group| 
|vic_race             |   Victim’s Race Description|
|vic_sex        |Victim’s Sex Description (D=Business/Organization, E=PSNY/People of the State of New York, F=Female, M=Male)|
|suspect_age_group    |  Suspect’s Age Group |
|suspect_race          | Suspect’s Race Description|
|suspect_sex            | Suspect’s Sex Description |
|hadevelopt        |If housing development of occurrence 1= yes, 0=no|

See [DataCleaning.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/DataCleaning.ipynb) to see how the data was cleaned fully.


## Exploratory Data Analysis

Most of the data features are categorical so we looked at several grouped bar charts. Here are some that are most interesting.

Location- Looking at the different areas of New York regardless of location, there are more Misdemeanors than other crimes. Brooklyn and Manhattan have the most.

![](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Images/newplot%20(1).png)

Time of Day - The time between 12pm-6pm there are more crime complaints 
![](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Images/newplot%20(5).png)


Race of Suspect - There is a large imbalance of crime complaints for suspects who are Black
![](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Images/newplot%20(6).png)

Sex of Victim - It is interesting to note how large Business/Organization crime complaints are
![](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Images/newplot%20(7).png)

A few of our initial thoughts of what features seem important look like they could be impactful in the model. We should note there is a fair amount of imbalanced data that could affect our overall model. 

For more in-depth data exploration see [ExploratoryDataAnalysis.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/ExploratoryDataAnalysis%20.ipynb)



## Model Prediction and Evaluation

THINGS TO ADD, what models did we test. 
Comparing the models
Most important features

## Conclusion

What we learned summerized and what next steps would be











1.	What research question are you trying to answer?

How well can features such as age, race, location, or time predict the severity of a crime?  Which features are most significant?

2.	What data are you planning on using and where are you going to get the data? 

We will be using New York City Historic Complaint data, dealing with all minor crimes (felony, misdemeanor, and violations) from 2006 to 2019. Some of the features in the original dataset will be too closely correlated with our target, so we are going to drop all columns except those we will be using for prediction.

3.	How much data wrangling or cleaning will be required?  Are you planning on making new features? 

The data wrangling will be fairly simple because we are pulling from an API. There will be some data cleaning required to deal with missing values. We will probably create a couple simple new features, such as turning time and date features into categories such as time of year and time of day.

4.	What types of EDA are you planning on doing? 

We will create plots of our features, including some geographical data which we are going to try to map. We will view summary statistics, identify outliers, and check what standard model assumptions are met. Using these tools will help us decide which model we will use.

5.	What kind of machine learning model will you most likely use?

This is a classification problem, so we are going to try Naïve Bayes, KNN, Gradient Boosting, then we will use cross validation and compare performance metrics to decide which model is the best for this dataset.

6.	What are your anticipated results?  Do you have a hypothesis? 

We predict that we will be able to classify the severity of a crime based on this data . We also predict that location and time will be very significant in prediction.

7.	Outline a plan of how everyone in the group is going to participate in this project. 

We are planning to participate equally with the data cleaning, EDA, modeling, scoring, and conclusion. In order to make sure we are keeping to workload as equal as possible, we will communicate regularly with a once/week meeting, and in text messages throughout the week.

8.	Who's GitHub account are you planning on using to host this project?

Kate Smith’s

