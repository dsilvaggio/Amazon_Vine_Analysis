# Amazon_Vine_Analysis
## Overview
An analysis of Amazon reviews written by members of the paid Amazon Vine program was performed using PySpark, SQL, and Amazon Web Services. The Amazon Vine Program allows manufacturers and publishers to recieve reviews for their products. Pet Product data was extracted, transformed, connected to an AWS RDS instance, and then loaded into pgAdmin. PySpark was the used to assess any bias towards favorable reviews from Vine members in the pet product data set.   
## Results
### ETL Process
An Amazon RDS was first created using AWS. A pgAdmin database was then created within the Amazon RDS server. Four tables were created within pgAdmin (customers_table, products_table, review_id_table, and vine_table) that match the Dataframes that are to be created using PySpark. The pet product data was then extracted and created into a new Dataframe. 
#### Customers_table
To create the customers_table dataframe, the groupby() function was used on the customer_id column of our initial Dataframe. The agg() function was chained to the groupby() function to create a column that showed the count of how many times a customer_id appeared in our initial Datframe. The counts column was renamed "cutomer_count". 
#### Product_table
The products_table dataframe was created by selecting the product_id and product_title columns from our initial Dataframe and then dropping any product_id duplicates. 
#### Review_id_table
The select() function was used on our initial Dataframe to select the review_id, customer_id, product_id, product_parent, and reivew_data columns from our initial Dataframe. These columns matched the columns that were created in the review_id_table within pgAdmin. The review_data column was also converted to a date object using the to_date() function within our select() function.
#### Vine_table
Lastly, the select() function was used again to retrieve the columns from our original Datframe that matched the columns created for our vine_table within pgAdmin. 

The above Dataframes were then loaded into pgAdmin and a query was ran to verify that the tables had been populated. 

### Determine Bias of Vine Reviews
1. Using PySpark, I was able to determint that there were 170 Vine reviews and 37,840 non-Vine reviews in the pet products dataset. 
2. 65 of the Vine reviews were 5 star reviews and 20,612 of the non-Vine reviews were 5 star reviews.
3. Using the above information, I was able to determine that about 38% of the Vine reviews were 5 star reviews and about 54% of the non-Vine reviews were 5 star reviews.  

## Summary
