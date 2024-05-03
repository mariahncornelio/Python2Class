# SANTANDER PRODUCT RECOMMENDATION KAGGLE PROJECT SOLUTIONS - PRACTICE 
This repository holds an attempt to apply machine learning and prediction-recommendation algorithms to Santander Bank's customer database using data from "Santander Product Recommendation"'zs Kaggle challenge: (https://www.kaggle.com/competitions/santander-product-recommendation/data?select=train_ver2.csv.zip).

# Overview
In this Kaggle Project, I was tasked to predict what a customer would buy and also recommend the top products they would want to buy based on things such as their previous purchases and customer backgorund and history from Santander Spain's customer database by the end of May 28, 2016. The approach in this repository includes machine learning algorithms such as logistic regression and gradient boosting decision tree and also item-based popularity recommendation based on frequency. The best model was able to come up with the top product recommended to the customer as well as their top 3 products based on the prediction score. 

# Summary of Work
## DATA
### Dataset Description
The data was 240.06 MB and contained 3 .zip files named "train.csv" for the training set, "test.csv" for the test set, and "sample_submission.csv" which gave a sample submission file in the correct format. The training set contains 13.6M rows and 48 columns and the testing set contains 929K rows and 24 columns. For the data fields, the columns were all in Spanish meaning I had to translate it to it's respective English description. The contents of the data spans from January 28, 2015 and lasts up until May 28, 2016 which is about 1.5 years of the customers behavior data from Santander Bank in Spain. 

### Data Preprocessing and Cleaning
- Translate the column names into English based on their respective data description found on the original challenge forum (i.e.: fecha_dato=calendar_date)
- Change columns to appropriate dates (dates to date/time, numbers/floats to integers, objects to strings, etc.
- Dropped the columns with the most amount of null values (last primary date and spouse index)
- Cannot just remove rows containing null values, therefore filled in empty cells in categorical values with the mode and empty cells in numerical values with the mean. If a binary variable column, filled it in with 0's

### Data Viz
First I defined boundaries such as income and age group so that it would be more efficient that way to aggregate the data by. Next, using the item-based recommendation algorithm based on sales frequency (amount of times it shows up), a table with a summary of each product is shown:

<img width="374" alt="Screen Shot 2024-05-03 at 3 48 30 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/72f53f1c-8fb3-48d6-ad34-9e12e19b9359">

Here we see that the top 3 products are current accounts, direct debits and particular accounts. 

<img width="862" alt="Screen Shot 2024-05-03 at 3 49 22 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/b8172bb2-262a-4dab-b779-939475b3d57b">


## PROBLEM FORMULATION
The problem of this dataset is that there is going to be a lot of changing variables. A person's preference will always change regardless if they are in the same income group or age group or similar living circumstances. So to solve this problem, I believe it is better to recommend products based on "previously purchased recommended items" or item similarity. Personally when I shop online, I tend to click the section that says "similar products to what you like" and end up spending more money because of that. To do this, we need to find the correlation between these the products. For this, I took math for data science so cosine similarity was done to compare 2 vectors (products) in this dataset and it sees if they are pointed in the same direction. 

<img width="653" alt="Screen Shot 2024-05-03 at 3 58 29 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/b739f50e-fc7a-4f61-9cc0-ba5bc1825258">


## TRAINING
For the model training, a logistic regression/gradient boosting decision tree was utilized. GBDT basically takes all decision trees and gets the top results from each of them to formulate a bigger result. These both have to do with correlation. This training only took 2k samples (to optimize performance and make it faster) from May 28, 2016 because this is what the question prompt asked for. A little more prepping was needed more because I did not realize there were inappropriate data types and more missing values beforehand. Training took a longer time because I was not sure what was wrong but it turns out the strings categories were not strings and the some of the intefers were still floats. There were also missing values in the "age_grouped" column so I filled null values using the category "adult." I tried rescaling because it told me to increase the number of iterations but I was not sure how to fix that part. 

## PERFORMANCE COMPARISONS
Through this algorithm, we were able to create a dataframe that contained the predicted probability each product would have for each customer. I created a submission file that took the top recommended product (pred_score > 0.5) for each customer ID and another submission file that took the top 3 recommended products (3 highest pred_score products). 

<img width="274" alt="Screen Shot 2024-05-03 at 4 11 52 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/b56809b8-eba6-491a-b386-90466c2bee3a">

<img width="381" alt="Screen Shot 2024-05-03 at 4 12 12 AM" src="https://github.com/mariahncornelio/DATA3402.Spring.2024.Fork/assets/143844081/52f4c786-7bee-4a55-bf79-6d1a6c03514a">


## CONCLUSIONS
- This took a long time to figure out
- Correlation algorithms (cosine similarity, LR, and algorithms like GBDT) are good for recommended product problems
- The top recommended product for many Santander customer's are "current accounts"
- Volatility of customer preferences as well as background and history had to be taken into account when creating the algorithm

## FUTURE WORK
- Try a different machine learning approach like SVM (but this takes forever)... maybe into two groups like popular and non-popular products based on these criterias
- Create stricter boundaries and criterias
- Create more data visualization graphs to help with visual aid analysis
  
# How to Reproduce Results
## OVERVIEW OF FILES IN REPOSITORY
- train_ver2.csv: provided model training file from Santander product recommendation Kaggle project
- test_ver2.csv: provided model testing file from Santander product reccommendation Kaggle product
- train_df_cleaned.csv: training dataframe after data preprocessing and cleaning
- test_df_cleaned.csv: testing dataframe adter data preprocessing and cleaning
- sample_submission.csv: provided sample submission file on what results should look like at the end
- final_product_submission.csv: submission file for top product by customer ID
- final_prod_top3_submission.csv: submission file for top 3 products by customer ID
- Data Preprocessing.ipynb: notebook for all data cleaning and preprocessing procedures
- Training and Testing.ipynb: notebook for all training and testing procedures

## SOFTWARE SETUP
For this project, I used Python3.11 and JupyterLab via the Anaconda app. 

## DATA
The data of this Kaggle project can be found here: (https://www.kaggle.com/competitions/santander-product-recommendation/data?select=train_ver2.csv.zip).

## TRAINING
To perform this training, make sure all floats are turned into integers, strings are strings, and no values are present. Create a product list using the product names given in the dataset and a features list taken from the remaining column names. Then create a column list that contains these two lists. Set X equal to your feature list and y equal to your product list and then split the training and the testing set using the 80-20 method (80% is used for training and 20% is used for testing). Create your logistical regression model and then fit it to your X and y variables. Do the same thing for the GradientBoostingClassifier() algorithm. Once done, create a dataframe with all the predictions and now you can create a function that takes the top reccommended product with prediction score greater than 0.5 and assigns the respective product to a customer ID. 

## PERFORMANCE EVALUATION
To evaluate a LR model, you can use an ROC/AUC curve where a higher X-axis shows a higher number of false positives rather than true negatives. 

# Citations
[1] Banco Santander. (2014). Santander Product Recommendation. Kaggle. https://www.kaggle.com/competitions/santander-product-recommendation/data?select=train_ver2.csv.zip 

[2] Bhandari, A. (2024). Guide to AUC ROC Curve in Machine Learning. Analytics Vidhya. https://www.analyticsvidhya.com/blog/2020/06/auc-roc-curve-machine-learning/#:~:text=In%20an%20AUC%2DROC%20curve,positives%20and%20False%20negatives%20naturally. 

[3] Mwiti, D. (2023). Gradient Boosted Decision Trees [Guide]: a Conceptual Explanation. Neptune.ai. https://neptune.ai/blog/gradient-boosted-decision-trees-guide#:~:text=In%20gradient%20boosting%2C%20an%20ensemble,average%20of%20all%20weak%20learners. 

[4] Sharadarao. (2023). Cosine Similarity. GeeksforGeeks. https://www.geeksforgeeks.org/cosine-similarity/ 

[5] Tabsharani, F. (2024). What is a support vector machine (SVM)? TechTarget. https://www.techtarget.com/whatis/definition/support-vector-machine-SVM#:~:text=A%20support%20vector%20machine%20(SVM)%20is%20a%20type%20of%20supervised,data%20set%20into%20two%20groups.

[6] Wang, D. (2017). 80%/20% splitting strategy for obtaining training, validation and testing sets. ResearchGate. https://www.researchgate.net/figure/80-20-splitting-strategy-for-obtaining-training-validation-and-testing-sets_fig1_320830045#:~:text=Instead%2C%20we%20choose%2080%25%2F,separately%20on%20the%20two%20sets. 

