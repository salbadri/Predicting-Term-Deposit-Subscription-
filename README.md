# Predicting Term Deposit Subscription 

This is Personal project. 

#### -- Project Status: [Completed]
## Project Intro/Objective
The goal of this project is to develop a robust model capable of predicting whether a client will subscribe to a term deposit. The project includes two main parts: Part 1 (Exploratory Data Analysis) and Part 2 (Training, Evaluation, and Testing).
 


## Project Description: 
### Dataset:
- The dataset used in this project was obtained from
[kaggle](https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets). 
It consists of 45,211 records and 17 variables, with a mix of continuous and categorical features. The dataset is imbalanced, as shown in the figure below:

![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/Original%20Dataset.png)


### Exploratory Data analysis (EDA): 
During the exploratory data analysis, the following steps were taken:

#### Multicollinearity Check:

       - For Continuous Features:

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/continous-correlation.png).

	- For Categorical Features (Association between Categorical features checked using Cramer V):
	
![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/CramerVAssociation.png)

- Unknown values in the dataset were replaced with 'nan' using NumPy (np.nan).
- The missing values were checked for randomness (missing at random) using the msno library and visualized with matrix and heatmap graphs.


![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msno-heatmap.png)

![github-small]( https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/msnoMatrix.png)

- The 'Poutcome' feature was dropped due to having 39,959 missing values, and the remaining rows with missing values were dropped.
- Outliers were detected using Z-score and boxplots for the features 'age,' 'balance,' 'pdays,' and 'previous.' Outliers were clipped at the 99th percentile.
- Box-Cox Transformation was applied to features 'age,' 'pdays,' 'balance,' 'duration,' and 'campaign.'
- Categorical features were converted to numeric using Label Encoder, and the training set was standardized. The test set was preprocessed similarly.

### Data Imbalance Treatment 

* The dataset was imbalanced, and three methods were tried to balance it: TomekLinks (tl), Nearmiss, and SMOTE. TomekLinks was found to be the most effective method.

![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/TomekLinks.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/NearMiss.png )
![github-small](https://github.com/salbadri/banking-Dataset-Marketing-Targets/blob/main/Images/Data%20Imbalance%20Treatment/SMOTE.png )

### Feature Sets 

Based on EDA, seven sets of features were defined to find the best set:

1. Original features
2. Original reduced (dropped 'pdays' and 'previous')
3. Clean-capped-features (contains capped features plus others that did not require capping)
4. Clean-trans-features (features that were transformed)
5. Clean-reduced-trans-features (dropped 'pdays,' 'previous,' and 'month')
6. Clean-cap-trans-features (features that were capped and transformed)
7. Clean-cap-trans-features reduced (dropped 'month,' 'pdays,' and 'previous')


### Part 2: 

In this section, the following steps were performed:

#### Used Algorithms

- Logistic Regression
- Support Vector Machine
- Decision Tree
- Histogram-Based Gradient Boosting
- Random Forest
- Voting Classifier (Estimators: Logistic Regression, Random Forest, and GaussianNB; Voting is soft)

#### Hyperparameter Tuning

GridSearch CV was used to find optimal hyperparameters with the following settings:
- CV = 5
- Scoring Metrics: F1, AUC
- Verbose = 3
- Error_score = Raise
- Refit: AUC

### Evaluation

All trained models were evaluated on the validation set, and the following metrics were calculated:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC AUC
- Latency

The best model was selected based on the ROC AUC score. Random Forest on the set of capped features achieved the best results.

[View Models Performance on Validation Set](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:l..)


### Results: 
Random Forest on Clean Capped Features achieved the best results among other models and feature set combinations. When evaluated on the test set, it achieved:

- Accuracy: 99.2%
- Precision: 96.4%
- Recall: 97.4%
- F1 Score: 96.9%
- ROC AUC: 98.4%

### Conclusion

Random Forest on Clean Capped Features outperformed other models and feature set combinations. Capping the features 'age,' 'balance,' 'duration,' 'campaign,' 'pdays,' and 'previous' improved the model's performance.

## Methods Used

- Inferential Statistics
- Machine Learning
- Data Visualization
- Predictive Modeling



## Technologies 
- Jupyter NoteBook
- [Tableau](https://public.tableau.com/views/Performanceofthemodelsonthevalidationset/Dashboard1?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link) (For Models Performance Visualization)

## Needs of this project

- data exploration/descriptive statistics
- data processing/cleaning
- statistical modeling

