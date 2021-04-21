# Optimizing_ML_Pipeline_Azure
# OVERVIEW

This projrct is part of the Udacity Azure ML Nanodegree. we build and optimize an Azure ML pipline using Azure ML python SDK.
training a Sikit-learn LogisticRegression model and tuning hyperparamter using Azure HyperDrive functionality.
this model is then compared to an Azure AutoML run.

# SUMMARY

The provided dataset is a markting Bank dataset and we have to predict wethear a client subscribed a term deposit.
we tuned the hyperparameter using HyperDrive then save the best model tuned by HyperDrive, next we use Automated Machine Learning
to get an opitimal model for the dataset, we then compared the two model and find out which result is better

# Scikit-learn Pipeline

We first retrieve a dataset from provided URL using AzureDataFactory class, then clean the data using clean_data method which contain
some preprocessing steps such as converting categorical variable, onehot encoding, etc.
After cleaning we split the dataset into train, test data.
Next we difine a Logistic Regression model for training.
Then we create a HyperDrive config passing to it a Sklearn estimator, paramter sampling and some other paramters.
The paramter we are using is the inverse regularization parameter and max_iter is the maximum number of iterations C and max_iter respectively.
For better efficiency we used a Early Stopping policy in HyperDrive config to terminate poorly performing runs.
I chose a BanditPolicy which is based on slack factor or slack amount and evaluation interval.
slack factor or slack amount will determine weather a primary metric run will terminate because its not within the specified slack factor or slack amount
Finally, we noted the best run and model from the HyperDrive run

# AutoML

Automated Machine learning can automate all the process involved in a Machine Learning project such as feature engineering, hyperparameter selection, model training.
First we need to define a AutoMLconfig object and setting various parameters such as which task to perform, training_data, label_column_name, etc.
next we submit the AutoMLconfig to start all the process mentioned above and it will try a bunch of models to determine the best outcome.
one thing worth remebring is that you need to pass a compute target to AutoMLconfig as a parameter so that you dont need to install dependency

# Pipeline comparison

Overall there is no big difference in accuracy between AutoML and HyperDrive, however whats interesting is that AutoML will try alot of model which is very hard
to do in HyperDrive because you need to define a pipline for every model you want to tune its hyperparameter 

AutoML accuracy is 0.9163 (VotingEnsemble), HyperDrive accuracy is 0.9167 (LogisticRegression)

# Future work

1 - try to balance the dataset, using stratified cross validation
2 - changing the paramter sampling method
3 - change cross validation 
4 - try diferent Termination policy
