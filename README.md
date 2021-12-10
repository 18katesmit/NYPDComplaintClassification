# NYPD Complaint Classification
Stat 426 Final Project

## Introduction
Crime across the United States is a constant part of life. However, in the past year and a half there has been a rise in understanding crime as it has to do with racial discrimination and other factors. Often, certain areas are over policed or certain crimes are dealt with more harshly based on factors that are not fully understood. While we cannot fully understand all factors that play apart in crime our project is trying to explore what affects the severity of a crime.

Using data found from historic New York Police Department (NYPD) [complaint report](https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i ) we are attempting to classify the severity of a crime, or offense level, based on features such as age, race, location, time of day, and sex for the NYPD.  The data used includes all valid felony, misdemeanor, and violation crimes reported to the NYPD from 2006 to the end of 2019. There are over 7 million different complaints but for this project we will only look at the last 50,000 complaints to ensure our machines can handle the data.

You should be able to easily reproduce our results from this repository, but you will need to request your own API key from Socrata.
https://support.socrata.com/hc/en-us/articles/115005364207
Alternatively, you can use the .csv file included in the repository.

We will use different classification machine learning models to learn from our data and then predict the offense level of a Misdemeanor, Felony, or Violation and see which features are the most significant in determining the severity. We think that age, race, and time of day might be factors that help predict severity more significantly than other features.

We will be using the following steps and have used several juypter notebooks in this repository to break up our work that can be easily followed:
1. Collecting and Cleaning the Data- found in  [DataCleaning.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/DataCleaning.ipynb)
2. Exploring the Data - found in [ExploratoryDataAnalysis.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/ExploratoryDataAnalysis%20.ipynb)
3. Model Prediction and Evaluation - found in [Model.ipynb](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Model.ipynb)

## Data Collection and Cleaning
As previously mentioned we used NYPD complaint data. We obtained our data using the Socrata API and got 50,000 of the results. From the inital read in from the API we have 40 different features for our data. Many of the features are redundant information, for example a written name of a station and a numerical number for the same station number, so we decided to drop them from the data. Additionally we dropped any feature that would inherently tell us the severity of the crime. 

After dropping columns we transformed our dates to only have the Month (1-12) and Time of day (4 different quarters). Additionally we turned the housing development names into a binary 1 or 0 to indicate if the complaint took place in a housing development. We standardized all entries that were labled as 'UNKNOWN' or 'U' to NaN. Lastly, we had to change our features that have ages to not include negative ages or values that were unreasonably high. 

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

For our classification models, we decided to use the methods of Bagging, gradient boosting, and a random forest classifier.

In the end, we found that gradient boosting yielded the most accurate model, with 56% accuracy, which is a 23% mporovement over a random guess. 

||precision|recall|f1-score|support|
|:-|:-|:-|:-|:-|
|FELONY|0.62|0.14|0.23|3127|
|MISDEMEANOR|0.56|0.93|0.70|5279|
|VIOLATION|0.51|0.16|0.25|1594|
||||||
|accuracy|||0.56|10000|
|macro avg|0.56|0.41|0.39|10000|
|weighted avg|0.57|0.56|0.48|10000|


But where our model really shines is not in prediction, because there is no practical reason to predict crime severity. Rather, looking at the importance of different features in our model can indicate what systemic and human biases exist in our police forces. From our most accurate model, we found that these were the ten features with most importance:

![](https://github.com/18katesmit/NYPDComplaintClassification/blob/main/Images/gbImportance.png)

The sex or classification of the victim is extremely important. Also, the sex and Race of the suspect proved to be important, particularly when the suspect was black. Additionally, it is clear that location plays a significant role in the severity of a crime, with crimes on the street, as well as longitude and latitude all being highly important to our models classifications. 

## Conclusion

What we learned summerized and what next steps would be










