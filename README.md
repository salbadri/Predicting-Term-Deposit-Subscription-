# Banking-Dataset-Marketing-Targets
Personal project. 
#### -- Project Status: [Completed]
## Project Intro/Objective
The goal of this project is to find robust model that can predict if the client will subscribe to a term deposit.
* There are two jupyter notbooks: part 1(Exploratory Data Analysis) and part 2 (Training, Evaluation, and Testing).

## Description of the Dataset:
The dataset was obtained from [kaggle](https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets). 
This dataset consists of 45211 records and 17 variables.

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

![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/Original%20Dataset.png)

* Has missing values: job, education, contact, and poutcome have unknown values. 


### Methods Used
* Inferential Statistics
* Machine Learning
* Data Visualization
* Predictive Modeling

## Project Description: 

### Part 1: Exploratory Data analysis (EDA): 
* Dataset has a mix of continuous and categorical features. I explored them separately. 
* Correlation between continuous features demonstrated below, pdays and previous are moderately correlated (r=0.45), campaign and day are weakly corelated (r=0.16). 
![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/continous-correlation.png)
* Association btween Categorical features checked using Cramer V
![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/CramerVAssociation.png)
* I replaced all unknowns in my dataset with ‘nan’ using numpy (np.nan). job has 288 Null values, education has 1857 Null values, contact has 13020 Null values, poutcome has 36959 Null values.

* Before treating missing values, I checked if they are missing at random using msno library. I used matrix and heatmap (see graph below); I concluded that they are missing at random. 
![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msno-heatmap.png)

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msnoMatrix.png)

* I dropped the feature Poutcome as it has 39959 missing values. For the rest I dropped every row that has missing values.

* I used Z-score and boxplot to detect outliers. Analysis showed that age, balance, pdays, and previous have outliers.  I clipped at the 99 percentiles. Saved results as capped to see if capping have impact on the performance of our models.
* I used Box-Cox Transformation. A Box Cox transformation is a transformation of non-normal dependent variables into a normal shape. Normality is an important assumption for many statistical techniques; if your data isn’t normal, applying a Box-Cox means that you are able to run a broader number of tests. I performed transformation on age, pdays, balance, duration, and campaign. 
* I converted categorical features to numeric using Label Encoder. And standardized my training set. I preprocessed the test set in the same way as I did with the training set. 
* Data set was already divided into train set and test set. I, then, partitioned the test set into test and validation. 
* My dataset is imbalanced. I Tried TomekLinks(tl), Nearmiss and SMOTE to balance my data. I found that TomekLinks was the best method. 
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/TomekLinks.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/NearMiss.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/SMOTE.png )
* Based on the EDA, I defined seven set of features:
1- Original features: original features (not capped or transformed).
2- original reduced: drop feature that I suspect it degrades the performance of my model. dropped pdays and previous as they are correlated. 
3- clean-capped-features: contains capped features in addition to other features that did not require capping.
4- clean-trans-features: contain features that were transformed. To check if transformation will improve the model performance. 
5- clean-reduced-trans-features: drop pdays and previous, month (month associated with housing)
6-clean-cap-tran features: contain features that were capped then transformed. To check if capping and transforming will improve performance of the model 
7- clean-cap-trans-features reduced: dropped month, pdays, and previous.


### Part 2: In this part I defined the algorithms that I am interested in. I trained the Algorithms and tuned the models using GridSearch CV. I, then, evaluate the models on the validation set; best performance model was evaluated on the test set

* Algorithms: 
1- Logistic Regression
2- Support Vector Machine
3- Decision Tree
4- Histogram Based Gradient Boosting
5- Random Forest
6- Voting Classifier: Estimators Logistic Regression, Random Forest, and GaussianNB. Voting is soft

* Tuning using GridSearch CV (Algorithms and the set Parameters):

I.Logistic Regression: penalty [l1, l2], tol [0.01, 0.001, 0.0001, 0.00001], max_iter[300, 400, 500, 600, 700, 1000]

II.Support Vector Machine: tol[0.1,0.01,0.001,0.0001], C [0.1,1,10]

III.Decision Tree: max_depth[5,10,15,30,50, None]


IV.Histogram Based Gradient Boosting: max_iter[100, 250, 500, 700, 1000, 1500], max_depth [1,3,5,7,9], and learning_rate [0.01,0.1,1]

V.Random Forest: n_estimators[100, 250, 500], max_depth[7, 10, None], bootstrap[True, False], 

VI.Voting Classifier: lr_C [0.1,1,10], lr_solver[saga], lr_maxiter[100, 200, 400, 500], rf_bootstrap[True, False]

* Scoring Matric: F1, and AUC
* CV: 5
* Verbose:3
* Error_score: Raise 
* Refit: AUC

* Evaluating the Models on the Validation set: all the trained models evaluated on the validation set. Accuracy, Precision, recall, F1 score, ROC AUC, and latency were calculated. Picked the best performance model based on ROC AUC score.  
Random Forest on the set of capped features achieved the best results. You can view models performance on validation set Here: [ModelsPerformance](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:l..)
	
* Best Model: Random Forest 
* Best set of Parameters: Bootstrap =False, n_estimators=500, max_depth= None
* Data Imbalance treated using TomkeLinks
* Best Set of Features: Clean Capped Features. It contains the following features: age_capped, job, marital, education, default, balance_capped, housing, loan, contact, day, duration_capped, campign_capped, pdays_capped, previous_capped)

* Results: when the model evaluated on the test set, it achieved:
 Accuracy: 99.2, Precision: 96.4, Recall: 97.4, F1 Score: 96.9, ROC AUC: 98.4

* Conclusion:
From the results we conclude that capping the features age, balance,duration, campign, pdays, and previous improved the performance of our model. 

## Technologies 
* Jupyter NoteBook
* [Tableau](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link) (For Models Performance Visualization)
## Needs of this project

- data exploration/descriptive statistics
- data processing/cleaning
- statistical modeling

