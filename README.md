# NYPDComplaintClassification
Stat 426 Final Project

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

