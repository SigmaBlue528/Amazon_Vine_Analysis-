Amazon Vine Analysis

The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. In this project, we will study a dataset holding reviews for shoes by completing the following steps:

•	Use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin.

•	Use PySpark to determine if there is any bias toward favorable reviews from Vine members in the dataset.

•	Write a summary of the analysis to submit to the SellBy stakeholders.

Objective:

•	In this project we will analyze Amazon reviews written by members of the paid Amazon Vine program to determine if there is any bias.

Resources:

•	Data Source: Amazon Shoes Reviews
•	Software: spark-3.2.3 - pgAdmin 4 - SQL - Google Colab Notebook - Amazon Web Services
•	Scripts: Amazon_Reviews_ETL.ipynb, Vine_Review_Analysis.ipynb, SchemaTesting.sql


Analysis of Data:

Perform ETL on Amazon Product Reviews

Using cloud ETL process, we have created an AWS RDS database with tables in pgAdmin, picked the shoes 
reviews dataset from Amazon Review Dataset and extracted the dataset in a DataFrame. After that we have transformed this DataFrame into 4 separate DataFrames that match the table schema in pgAdmin.Finally, we have uploaded the transformed data into the appropriate tables and ran queries in pgAdmin to confirm that the data has been uploaded 

Table 1 - The customers _table DataFrame:

 

Table 2 - The products_table DataFrame:

 

Table 3 - The review_id_table DataFrame:

 

Table 4 - The vine_table DataFrame:

 

Determine Bias of Vine Reviews:

Using PySpark we have extracted the same dataset in a new Google Colab Notebook Vine_Review_Analysis.ipynb . We have recreated the vine_table (Table 4) and we have performed the following steps:

•	Created a new DataFrame to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors.

•	Filtered the new DataFrame and created a new DataFrame to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.

•	Filtered the later DataFrame and created a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program/paid (Table 5), and another one where the review was not part of the Vine program/unpaid (Table 6)


Table 5 - Paid Reviews DataFrame

 

Table 6 – Unpaid Reviews DataFrame

 

•	In the last part, we have calculated the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for paid and unpaid program


Results and Summary:

Based on our analysis, we have found the following:

•	The total number of Vine reviews is 22, while the total number of reviews for unpaid program is 26987.
•	The number of 5-star reviews for paid program is 13 while it's 14475 for unpaid program.
•	The percentage of 5-star reviews for paid program is: 0.59% which is so close to the percentage of 5-star reviews for unpaid program: 0.53%

Even if the percentage of 5-star reviews for paid and unpaid program is close one should consider the existence of a bias for reviews in the Vine program due to the considerably big difference between the total number of Vine reviews and non-Vine reviews; In other words, the number of Vine reviews is a not even close to 1% of that of the non-Vine reviews. I would suggest performing a T-test to make sure if there's a statistical difference between the mean of the sample and population distribution.

