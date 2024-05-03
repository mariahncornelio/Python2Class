# SANTANDER PRODUCT RECOMMENDATION KAGGLE PROJECT SOLUTIONS
This repository holds an attempt to apply machine learning and prediction-recommendation algorithms to Santander Bank's customer database using data from "Santander Product Recommendation"'zs Kaggle challenge: (https://www.kaggle.com/competitions/santander-product-recommendation/data?select=train_ver2.csv.zip).

# Overview
In this Kaggle Project, I was tasked to predict what a customer would buy and also recommend the top products they would want to buy based on things such as their previous purchases and customer backgorund and history from Santander Spain's customer database by the end of May 28, 2016. The approach in this repository includes machine learning algorithms such as logistic regression and gradient boosting decision tree and also item-based popularity recommendation based on frequency. The best model was able to come up with the top product recommended to the customer as well as their top 3 products based on the prediction score. 

# Summary of Work
## DATA
### Dataset Description
The data was 240.06 MB and contained 3 .zip files named "train.csv" for the training set, "test.csv" for the test set, and "sample_submission.csv" which gave a sample submission file in the correct format. The training set contains 13.6M rows and 48 columns and the testing set contains 929K rows and 24 columns. For the data fields, the columns were all in Spanish meaning I had to translate it to it's respective English description. The contents of the data spans from January 28, 2015 and lasts up until May 28, 2016 which is about 1.5 years of the customers behavior data from Santander Bank in Spain. 

### Data Preprocessing and Cleaning
- Translate the column names into English based on their respective data description found on the original challenge forum (i.e.: fecha_dato=calendar_date).
- Change columns to appropriate dates (dates to date/time, numbers/floats to integers, objects to strings, etc.
- Dropped the columns with the most amount of null values (last primary date and spouse index). 
- Cannot just remove rows containing null values, therefore filled in empty cells in categorical values with the mode and empty cells in numerical values with the mean. If a binary variable column, filled it in with 0's

### Data Viz
First I defined boundaries such as income and age group so that it would be more efficient that way to aggregate the data by. Next, using the item-based recommendation algorithm based on sales frequency (amount of times it shows up), a table with a summary of each product is shown:
<img width="374" alt="Screen Shot 2024-05-03 at 3 48 30 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/72f53f1c-8fb3-48d6-ad34-9e12e19b9359">
Here we see that the top 3 products are current accounts, direct debits and particular accounts. 
<img width="862" alt="Screen Shot 2024-05-03 at 3 49 22 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/b8172bb2-262a-4dab-b779-939475b3d57b">

## PROBLEM FORMULATION
The problem of this dataset is that 

## TRAINING

## PERFORMANCE COMPARISONS

## CONCLUSIONS

## FUTURE WORK

# How to Reproduce Results
## OVERVIEW OF FILES IN REPOSITORY

## SOFTWARE SETUP

## DATA

## TRAINING

## PERFORMANCE EVALUATION

# Citations

