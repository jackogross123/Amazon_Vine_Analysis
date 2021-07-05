# Amazon Vine Analysis

## Overview of the Analysis

In this analysis, we are looking at Amazon reviews written by members of the Vine program. Our company SellBy is looking to pay a fee to Amazon to use the Vine program to publish reviews to boost sales. The Amazon Vine program is a service that allows individuals to recieve reviews for their products.

We want to explore any positive or negative bias in the Amazon Vine reviews. We are going to be analyzing data from the AMazon outdoor department. To accomplish this goal, we will perform an ETL process on the Data and connect to an AWS RDS instance. Then we will use PySpark to figure out if there are any bias' to the paid reviews.

### Analysis Resources
Notebooks: [Amazon_Reviews_ETL](https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb), [Vine_Review_Analysis](https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb)
Software: Google Collab Notebook, Amazon Web Services, PostgreSQL 13
Data Sources [Amazon Outdoor Product Reviews](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Outdoors_v1_00.tsv.gz)

## Results of the Analysis

Here are screen shots from all of the Dataframes we created in deliverable one.

<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/review_id_table.png" width="700" >

<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/products_table.png" width="700" >

<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/customers_table.png" width="700" >

<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/vine_table.png" width="700" >

### Vine and non-Vine Reviews
[Amazon Outdoor Product Reviews] dataset contained over 2 million total reviews. Because we wanted to determine bias of the vine reviews, we need to filter the reviews to find ones that users thought were helpful.To narrow it down further, we retrieved all the rows in the dataframe where helpful reviews were 50%. Here is the dataframe.

#### First Filtered Dataframe
<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/step_1.png" width="700" >

#### Second Filtered Dataframe
<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/step_2.png" width="700" >

Using this df, we could filter it once more to find out how many of those reviews were part of the Amazon Vine Program (paid). vine_paid_helpful_df = vine_helpful_votes_df.filter("vine == 'Y'"). Using this filtered dataframe, we determined that there were 107 paid reviews for outdoor products out of 39,976 total.

#### Vine (Paid) Filtered Dataframe
<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/step_3.png" width="700" >

#### Non-Vine (Unpaid) Filtered Dataframe

For non-Vine Program reviews, we simply changed the filter from Y to N. Using this filtered dataframe, we found that there were 39,869 unpaid reviews for outdoor products out of 39,976 total.

<img src="https://github.com/jackogross123/Amazon_Vine_Analysis/blob/main/Resources/step_4.png" width="700" >

### 5-Star Ratings of Vine and non-Vine Reviews

To further explore bias in reviews, we wanted to determine if Vine reviewers gavr 5-star ratings more often than non-Vine. We filtered it again by the vine column, Y and N, similar to what we did in the last section.

There were a total of 21,061 5-star reviews, of those, 56 were paid and 21,005 were Vine. Vine people were much more likely to give a 5 star review. However, it's important to study the percentages of good votes to overall votes to determine if the percentages are the same.

### Percent 5-Star Ratings of Vine and non-Vine Reviews

To complete our bias analysis, we needed to see what percent of the total Vine and non-Vine reviews were 5-star reviews and compare. Using the variables we calculated in previous steps, we determined the following percentages:

#### % 5-Star Vine Reviews of Total
56 out of 107 Reviews = 52.34%

#### % 5-Star non-Vine Reviews of Total
21,005 out of 39,869 Reviews = 52.69%

Given these results, Vine reviews have the same liklehood of giving a 5-star review. There doesn't appear to be any bias.

### Additional Analysis

To further this conclusion, we wanted to find out just how small of sample the 5-star Vine reviews were among all 5-star reviews.

##### % 5-Star Vine Reviews of Total 5-Star
56 out of 21,061 Reviews = 0.27%

##### % 5-Star Vine Reviews of Total 5-Star
21,005 out of 21,061 Reviews = 99.73%

Because 5-star Vine reviews represent a small portion 0.27% of all 5-star reviews, they are unlikely to have create positivity bias for reviews on the entire dataset. We could also look at the summary stats to see if there is an irregular doistribution of teh data.
