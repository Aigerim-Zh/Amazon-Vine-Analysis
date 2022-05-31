# Amazon-Vine-Analysis

# Project Overview
In this project, I am tasked with analyzing Amazon reviews written by members of the paid Amazon Vine program. 

The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. 

In this project, I have access to approximately 50 datasets. Each one contains reviews of a specific product from clothing apparel to wireless products. I will pick one of these datasets and use ```PySpark``` to perform the ETL process to extract, transform, connect the dataset to an ```AWS RDS``` instance, and load the transformed data into ```pgAdmin```. 

Then, I will use ```PySpark``` to determine if there is any bias toward favorable reviews from Vine members in our dataset. 

# Results

# Deliverable 1. Perform ETL on Amazon Product Reviews
The code for this deliverable: [Amazon_Reviews_ETL.ipynb](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Amazon_Reviews_ETL.ipynb)

- For this project, I chose to work with the "Electronics" category dataset. 
- I created a database with Amazon RDS. 
- ```PostgreSQL 13.4-R1``` is used as an engine for this database. So, I connected ```pgAdmin``` to the ```AWS RDS``` instance.
- Then I run the database schema ([challenge_schema.sql](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/challenge_schema.sql)) in the Query Tool to create four tables: ```customers_table```, ```products_table```, ```review_id_table```, and ```vine_table```.
- Next, as we are dealing with millions of observations, I uploaded [Amazon_Reviews_ETL.ipynb](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Amazon_Reviews_ETL.ipynb) as a ```Google Colaboratory``` notebook to import PySpark libraries and connect to the AWS RDS instance and export tables to Postgres.
- After extracting my dataset of choice, I transformed it into four DataFrames that match the schema in the pgAdmin tables.

## The customers_table DataFrame
![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/customers_df_table.png)

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/sql_customers_table.png)


## The products_table DataFrame
![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/products_df_table.png)

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/sql_products_table.png)

## The revew_id_table DataFrame

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/review_id_df.png)

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/sql_review_id_table.png)


## The vine_table DataFrame
![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/vine_df.png)

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/sql_review_id_table.png)


# Deliverable 2. Determine Bias of Vine Reviews

The code for this deliverable: [Vine_Review_Analysis.ipynb](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Vine_Review_Analysis.ipynb)

In this deliverable, I examined if there is any bias towards reviews that were written as part of the Vine program, in other words, if having a paid Vine review makes a difference in the percentage of 5-star reviews.

I followed the following steps to get the final result:
* Extracted the dataset from the previous deliverable and dropped all non-existent values.

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/dropna_df.png)

* Exported the vine_table from the previous deliverable.

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/vine_df_del2.png)

* To ensure that the results are representative, I focused on reviews with 20 or more total vote counts. 

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/total_votes_20_or_more.png)


* Then, further filtered the dataset to the percentage of helpful votes equal to or greater than 50. 

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/helpful_votes_50%25.png)

* Then created two separate datasets for reviews that were and were not written as part of the Vine program.  

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/paid_df.png)

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/non_paid_df.png)

## Results 

![](https://github.com/Aigerim-Zh/Amazon-Vine-Analysis/blob/main/Images/Deliverable%202/Results.png)

### How many Vine reviews and non-Vine reviews were there?

There are in total 1080 and 49,659 Vine- and non-Vine members, respectively. Reviews from Vine members constitute a small percentage of total reviews (2.1%).

### How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
- 454 out 1080 reviews from Vine members were 5-star reviews
- Non-Vine members left 23,034 5-star reviews out of 49,659 total reviews.

### What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
- 42% of Vine member reviews
- 46.4% of non-Vine member reviews

# Summary
Based on the findings above, there appears to be no bias towards reviews written by Vine members. Interestingly, the percentage of 5-star reviews among Vine members is slightly lower than that for non-Vine members. This may mean that Vine members are slightly more critical than regular reviewers.

However, to support this assumption, a series of statistical tests need to be run. Also, it is important to test whether the same result remains across all product lines. 


