# Amazon_Vine_Analysis
## Overview
An analysis of Amazon reviews written by members of the paid Amazon Vine program was performed using PySpark, SQL, and Amazon Web Services. The Amazon Vine Program allows manufacturers and publishers to receive reviews for their products. Pet Product data was extracted, transformed, connected to an AWS RDS instance, and then loaded into pgAdmin. PySpark was used to assess any bias towards favorable reviews from Vine members in the pet product data set. 
### Resources/Tools
- [Amazon Vine Data](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Pet_Products_v1_00.tsv.gz)
- Apache Spark - pySpark
- Postgres
- Python
- AWS

## Results
### ETL Process
An Amazon RDS was first created using AWS. A pgAdmin database was then created within the Amazon RDS server. 

![This is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-09%20at%209.48.09%20AM.png)

Four tables were created within pgAdmin (customers_table, products_table, review_id_table, and vine_table) that match the Dataframes that are to be created using PySpark. The pet product data was then extracted and created into a new Dataframe which can be seen below.

![this is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-11%20at%209.26.17%20PM.png)
#### Customers_table
To create the customers_table Dataframe, the groupby() function was used on the customer_id column of our initial Dataframe. The agg() function was chained to the groupby() function to create a column that showed the count of how many times a customer_id appeared in our initial Datframe. The "count" column was renamed "cutomer_count".

![this is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-11%20at%209.28.30%20PM.png)
#### Product_table
The products_table Dataframe was created by selecting the product_id and product_title columns from our initial Dataframe and then dropping any product_id duplicates. 

![This is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-11%20at%209.29.24%20PM.png)
#### Review_id_table
The select() function was used on our initial Dataframe to select the review_id, customer_id, product_id, product_parent, and reivew_data columns from our initial Dataframe. These columns matched the columns that were created in the review_id_table within pgAdmin. The review_data column was also converted to a date object using the to_date() function within our select() function.

![This is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-11%20at%209.29.37%20PM.png)
#### Vine_table
Lastly, the select() function was used again to retrieve the columns from our original Datframe that matched the columns created for our vine_table within pgAdmin.

![This is an image](https://github.com/dsilvaggio/Amazon_Vine_Analysis/blob/main/Resources/Screen%20Shot%202022-06-11%20at%209.29.47%20PM.png)

#### Load into pgAdmin
The above Dataframes were then loaded into pgAdmin and a query was run to verify that the tables had been populated.

### Determine Bias of Vine Reviews
1. Using PySpark, I was able to determine that there were 170 Vine reviews and 37,840 non-Vine reviews in the pet products dataset. 
2. 65 of the Vine reviews were 5-star reviews and 20,612 of the non-Vine reviews were 5-star reviews.
3. Using the above information, I was able to determine that about 38% of the Vine reviews were 5-star reviews and about 54% of the non-Vine reviews were 5-star reviews.  

## Summary
Based on the above findings, there is a positivity bias for reviews in the Vine program. Only 38% of Vine reviews were 5-star reviews versus the 54% of non-Vine reviews. One additional analysis that I could perform with the Vine dataset to support this statement would be to calculate the measures of central tendency (mean, median, mode) as well as the measures of spread (standard deviation, variance, IOR). By comparing the differences in these statistical measures, we would be able to further verify any positivity bias for reviews in the Vine program.  
