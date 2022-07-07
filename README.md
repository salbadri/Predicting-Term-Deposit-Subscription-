# Banking-Dataset-Marketing-Targets
This is a personal project. 
#### -- Project Status: [Completed]
## Project Intro/Objective
I aim to find a robust model that can predict if the client will subscribe to a term deposit.

This project has two jupyter notbooks: part 1 and part 2.
* Part 1: Exploratory Data analysis (EDA): I explored the data and performed the necessary cleaning. 
* Part 2: Training Algorithms and then evaluate the models on the validation set; best performance model was evaluated on the test set
## Description of the Dataset:
The dataset obtained from kaggle.It consists of 45211 records and 17 variables. Tables below has a description of the variables.

|Variables |Type | Description
------- | ------- | ------- 
|Age | numeric | age of the client 
| Job | categorical | management, technician, entrepreneur, blue-collar, unknown, retired, admin., services, self-employed, unemployed, housemaid, student
| marital |categorical | married, single, divorced
| education |categorical | tertiary, secondary, unknown, primary
| default | categorical | no, yes
| Balance | numeric | average yearly balance, in euros 
| housing | categorical | no, yes
| loan | categorical | no, yes
| contact | categorical| unknown, cellular, telephone
| Day | numeric | last contact day of the month (1 to 31)
| Month | categorical| may, jun, jul, aug, oct, nov, dec, jan, feb, mar, apr
| Duration | numeric | last contact duration, in seconds (numeric)
| Campaign | numeric| number of contacts performed during this campaign and for this client (numeric, includes last contact)
| pdays | numeric | number of days that passed by after the client was last contacted from a previous campaign (numeric, -1 means client was not previously contacted)
| previous | numeric | number of contacts performed before this campaign and for this client
| poutcome | categorical | outcome of the previous marketing campaign: unknown, failure, other, success
| Y (target variable |categorical| has the client subscribed a term deposit? ('yes', 'no')

## Issues with Dataset
* Imbalanced as it depicted in the figure below

![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Dist%20of%20the%20target%20variable%20.png)

* Has missing values: job, education, contact, and poutcome have unknown values. 








### Methods Used
* Inferential Statistics
* Machine Learning
* Data Visualization
* Predictive Modeling

## Project Description

 
## Needs of this project

- data exploration/descriptive statistics
- data processing/cleaning
- statistical modeling

