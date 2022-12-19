
#B9DA108 Programming for Data Analysis (B9DA108_2223_TMD1S)

Primary objective: To design and develop a Data Acquisition and Preprocessing Pipeline.

Task:You are required to develop a Data Acquisition and Preprocessing Pipeline of your choice, including data acquisition (API, Web scraping, DB Extract etc.), Extraction of features and Transformations as appropriate, followed by loading into an appropriate database. The focus of the complexity of the pipeline is your choice.

Dataset:
dataset 2 Police stop data, link to dataset-https://services.arcgis.com/afSMGVsC7QlRK1kZ/arcgis/rest/services/Police_Stop_Data/FeatureServer/0/query?where=1%3D1&outFields=*&outSR=4326&f=json

The dataset was taken from open dataset website by Minneapolis government. It contains data of traffic law enforcements from 2016 to 2021 with more than 1,70,000 entries. Minneapolis police department update the dataset each day with the new data. From the below figure Fig.2, all fields in the dataset are visible. Here the field `OBJECTID` is the unique one for each entry. The dataset contains details like time, location, race, gender, the actions police taken each time and problem caused.

#Data Management
MongoDB is used as the primary data storage method since, the data from APIs contain unstructured data. MongoDB accepted unstructured JSON data, and it has the ability fetch without any hassle. In addition to that, MongoDB can handle large volume of data better than normal relational databases.  Our datasets are very large in size and it’s better to store these data in MongoDB.
•	The MongoDB collection is imported to the pandas Dataframe using MongoDB’s find method.

•	There were many unwanted fields which have trivial importance in our analysis. They were additional geographical data other than co-ordinates, prerace, callDisposition, x, y, masterIncidentNumber, lastUpdateDate and _id. OBJECTID is the unique identifier of the data, so the field masterIncidentNumber is not required. Also, field lastUpdateDate is irrelevant in this analysis.

•	The dataframe is comparatively large and contains lot of null values. So, first rows with null value of race fields are removed. The removed rows are archived in another collection named `errorCollection` in MongoDB for future references.

•	Next, removed all the null values in the dataset to make it cleaner.

•	Fields like `gender` and `race` have `Unknown’ as value in the dataframe. Rows with `Unknown` value are also removed.

•	The `reason’ field has empty string as value in many rows. Those empty rows also removed.

•	The field policePrecinct was in string format. It has values from 1 to 5. It is changed to integer format for easiness. 

•	After the cleaning, the count of rows of the dataframe reduced to 99718.

•	The date field was in UNIX timestamp format, so, I split the date into day, month and year format and saved in new columns for visualization and analysis. 

•	The values of `problem` field, a major column in the dataset, has lengthy and irrelevant values. All the values are transformed to short meaningful words for better understanding.


 From the studies,its clear that Black community is more involved in the police actions. Over 50% incidents are related to Black and African people
