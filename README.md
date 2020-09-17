# Financial-Texts-Analysis-In-US-Securities-and-Exchange-Commision-Analysis-index.md

![alt text](ussec.PNG)

### Table of contents
* [Introduction](#introduction)
* [Problem Statement](#problem-statement)
* [Data Source](#data-source)
* [Technologies](#technologies)
* [Type of Data](#type-of-data)
* [Data Pre-processing](#data-pre-processing)
* [Algorithms Implemented](#algorithms-implemented)
* [Steps Involved](#steps-involved)
* [Evaluation Metrics](#evaluation-metrics)
* [Results and Conclusion](#results-and-conclusion)

### Introduction
Objective of this assignment is to extract some sections (which are mentioned below) from SEC / EDGAR financial reports and perform text analysis to compute variables those are explained below. Link to SEC / EDGAR financial reports are given in excel spreadsheet “cik_list.xlsx”. 

Please add https://www.sec.gov/Archives/ to every cells of column F (cik_list.xlsx) to access link to the financial report. 
Example: Row 2, column F contains edgar/data/3662/0000950170-98-000413.txt
Add https://www.sec.gov/Archives/ to form financial report link i.e. 
https://www.sec.gov/Archives/edgar/data/3662/0000950170-98-000413.txt 

### Problem Statement
* Build data pipeline to extract the Financial Texts from the US Security and Exchange Commissions website and perform NLP operations on the text. 

### Data Source
* The Dataset was obtained from the website US Security and Exchange Commisions Website: 
https://www.sec.gov/Archives/edgar/data/3662/

### Technologies
* Python 3.6.7

### Type of Data
* The data set consists of 150 records which has links provided to the US Security and Exchange Commissions Financial documents.
* The data does not contain any null values

### Data Pre-processing
* Tokenizing, removal of stop words and stemming was done for textual data

### Tools Implemented
* Vedar Rule-based model
* Pandas
* NLTK
* BeautifulSoup

### Steps Involved

## Technique 1 - K-Means(Context Based Filtering)
* Based on the reviews obtained above we have created its TF-IDF using TfidfVectorizer function.
* Since we are handling huge amount of data with our data frame having 5,074,160 reviews we have done rest of the operations in Apache Spark for efficient and faster handling of big data. We have created a Spark data frame from the pandas reviews data frame
* Next we have created a data cleaning pipeline using the Pipeline function in which we have cleaned the spark data frame by tokenizing the reviews, removing stop words, calculated the term frequencies (TF) and IDF for the tokenized words.
* We have clustered the products. So now whenever a new input keyword has been searched, it would pass through pipeline for cluster assignment. Products under the respective cluster are up for recommendation.

## Technique 2 - ALS Collaborative Filtering Algorithm
* We have obtained a Spark data frame containing item id, user id and ratings
* Alternating Least Squares algorithm requires the inputs to be numerical and integers with value less than 2,147,483,647 (32-bit limit). So we have created new index for      item_id and user_id using StringIndexer with definitive mapped values for each user and item.
* We have split the data into (80%) training and (20%) testing. We have used ALS (Alternating Least Squares) algorithm for training the data.
* We have evaluated the model on the test data. We have got RMSE value of 1.134. We thought that it might be over fitting the data so we implemented 5-fold Cross Validation in the next step.
* After implementing 5-fold ALS Cross Validation and evaluating on the test data we have obtained a RMSE value of 0.8345 which showed an improvement from the previous time.
* Finally, using our model we are obtaining TOP 10 recommendations for all the users in our data frame.
  
### Evaluation Metrics  
RMSE (Root Mean Square Error) 

### Results and Conclusion
By analyzing our dataset through various tools like R, Python, Pyspark we developed a product recommendation system based on the customer’s interest. We have used 2 different models for this purpose i.e. KNN and ALS Collaborative Filtering.

For the KNN which does context based filtering, we have tested our model with a test data which shows products under their respective cluster. It shows the products which are closely related to Kit Kat.

![alt text](rec_res1.JPG)

On implementing the ALS Collaborative Filtering Algorithm, we have used ALS model in which we have obtained RMSE value of 1.134.

![alt text](rec_res2.JPG)

On using 5-fold cross validation and evaluating on the test data the RMSE value showed an improvement. We obtained RMSE value of 0.8345.

![alt text](rec_res3.JPG)
