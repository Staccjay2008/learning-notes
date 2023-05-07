#### Step1 - Set up environment
- Run the pip install in your Python IDE.

```SQL
pip install -r requirements.txt

```

#### Step2 - Run code

- Run Python_code.py file.

#### Step3 - Output the final result
- Py file will generate final_result.csv file.

#### Explanation of the code
##### Test_sqlite_connection() 
- Test_sqlite_connection is used to test the connection to assay-results.db from company 2. It is my starting point.
- In this function, I check the connections and browse the tables inside the database

##### combine_company2_data() 
- combine_company2_data is to create a table to store data from all 3 companies.
- I define the right schema and join 2 tables - assay and sample to get the result.
- In this step, 3 records get filtered out because of the inner join.
- The reason I use inner join is long, lat is very important if the data is missing, then it is not useful to keep them.
- load the data into combined_data.

##### combine_company3_data() 
- combine_company3_data only needs to deal with 1 file - assays.csv.
- column names have white space in it (remvoe the space).
- I convert the columns such as silicon_dioxide_percentage and titanium_dioxide_percentage into rows.
- load the data into combined_data.

##### combine_company1_data()
- both assay_samples and chemical_compositions have error or bad lines in it.
- I skip the bad lines and only keep the good ones. (before the data is not reliable is format is off).
- I merge the 2 tables into one table using the common key sample_id.
- I split lat_long into 2 seperate columns and change the data type to float.
- load the final result into combined_data.


##### clean_data()
- clean_data is to clean the data based on the value range
- I only get records that lat between -90 and 90
- long between -180 and 180 
- total_mineral_composition is NULL or between 0 and 100

##### Note:
- 3 companies may use the same id, so I add another column company to differentiate the records.
- only company 1 has total_mineral_composition. I don't want to lose the data. Therefore, for company 2 and 3, I make the value as NULL for total_mineral_composition.


