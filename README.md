# Predicting Term Deposit Subscription 


Personal project. 
#### -- Project Status: [Completed]
## Project Intro/Objective
The goal of this project is to find robust model that can predict if the client will subscribe to a term deposit. I started with exploratory data analysis EDA.  Based on the EDA, I planned dataset cleaning, what algorithms to utilize, and defined sets of features.   
* There are two jupyter notbooks: part 1(Exploratory Data Analysis) and part 2 (Training, Evaluation, and Testing).

## Project Description: 
### Dataset:
* The dataset was obtained from [kaggle](https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets). 
This dataset consists of 45211 records and 17 variables.  Dataset has a mix of continuous and categorical features

* Dataset is imbalanced as it depicted in the figure below

![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/Original%20Dataset.png)


### Exploratory Data analysis (EDA): 
* I checked for multicollinearity 
	* Continous Features:

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/continous-correlation.png).

	* Categorical Features (Association btween Categorical features checked using Cramer V):
	
![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/CramerVAssociation.png)

* I replaced all unknowns in my dataset with ‘nan’ using numpy (np.nan). And, I checked if they are missing at random using msno library. I used matrix and heatmap (see graphs below); I concluded that they are missing at random. 

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msno-heatmap.png)

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msnoMatrix.png)

* I dropped the feature Poutcome as it has 39959 missing values. For the rest I dropped every row that has missing values.

* I used Z-score and boxplot to detect outliers. Analysis showed that age, balance, pdays, and previous have outliers.  I clipped at the 99 percentiles. 

* I used Box-Cox Transformation. A Box Cox transformation is a transformation of non-normal dependent variables into a normal shape. Normality is an important assumption for many statistical techniques; if your data isn’t normal, applying a Box-Cox means that you are able to run a broader number of tests. I performed transformation on age, pdays, balance, duration, and campaign. 

* I converted categorical features to numeric using Label Encoder. And standardized my training set. I preprocessed the test set in the same way as I did with the training set. 

* My dataset is imbalanced. I Tried TomekLinks(tl), Nearmiss and SMOTE to balance my data. I found that TomekLinks was the best method. 
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/TomekLinks.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/NearMiss.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/SMOTE.png )
* Based on the EDA, I defined seven set of features (we aim to find the best set of features):
	* Original features: original features (not capped or transformed).
	* original reduced: drop feature that I suspect it degrades the performance of my model. dropped pdays and previous as they are correlated. 
	* clean-capped-features: contains capped features in addition to other features that did not require capping.
	* clean-trans-features: contain features that were transformed. To check if transformation will improve the model performance. 
	* clean-reduced-trans-features: drop pdays and previous, month (month associated with housing)
	* clean-cap-tran features: contain features that were capped then transformed. To check if capping and transforming will improve performance of the model 
	* clean-cap-trans-features reduced: dropped month, pdays, and previous.


### Part 2: In this part I defined the algorithms that I am interested in. I trained the Algorithms and tuned the models using GridSearch CV. I, then, evaluate the models on the validation set; best performance model was evaluated on the test set

* Used Algorithms: 
	* Logistic Regression
	* Support Vector Machine
	* Decision Tree
	* Histogram Based Gradient Boosting
	* Random Forest
	* Voting Classifier: Estimators Logistic Regression, Random Forest, and GaussianNB. Voting is soft

* I utilized GridSearch CV to find the optimal hyperparameters. I set CV =5, Scoring Matric: F1, and AUC,  Verbose = 3, Error_score= Raise , and Refit: AUC



### Evaluation:

All the trained models evaluated on the validation set. Accuracy, Precision, recall, F1 score, ROC AUC, and latency were calculated. Picked the best performance model based on ROC AUC score.  
Random Forest on the set of capped features achieved the best results. You can view models performance on validation set Here: [ModelsPerformance](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:l..)
	

### Results: 
Best Model is Random Forest. And, best set of features is Clean Capped Features.  
when the model (Random Forest on Clean Capped Features) evaluated on the test set, it achieved:
 Accuracy: 99.2, Precision: 96.4, Recall: 97.4, F1 Score: 96.9, ROC AUC: 98.4
 
### Conclusion:
Random Forest on Clean Capped Features achieved the best results among other models - feature sets  combinations. From the results we conclude that capping the features age, balance,duration, campign, pdays, and previous improved the performance of our model. 

### Methods Used
* Inferential Statistics
* Machine Learning
* Data Visualization
* Predictive Modeling

## Technologies 
* Jupyter NoteBook
* [Tableau](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link) (For Models Performance Visualization)

## Needs of this project

- data exploration/descriptive statistics
- data processing/cleaning
- statistical modeling

