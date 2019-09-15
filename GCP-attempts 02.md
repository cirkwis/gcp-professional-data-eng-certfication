**Which of these open source frameworks is best suited to process simultaneous batch and streaming in a single data pipeline?**

- Apache Beam

**2. Your production Bigtable instance is currently using four nodes. Due to the increased size of your table, you need to add additional nodes to offer better performance. How should you accomplish this without the risk of data loss?**

- Edit instance details and increase the number of nodes. Save your changes. Data will re-distribute with no downtime.

**3. You are designing a relational data repository on Google Cloud to grow as needed. The data will be transactionally consistent and added from any location in the world. You want to monitor and adjust node count for input traffic, which can spike unpredictably. What should you do?**

- Use Cloud Spanner for storage. Monitor CPU utilization and increase node count if more than 70% utilized for your time span: This is correct because of the requirement for globally scalable transactions—use Cloud Spanner. CPU utilization is the recommended metric for scaling

**4. You are designing storage for CSV files and using an I/O-intensive custom Apache Spark transform as part of deploying a data pipeline on Google Cloud. You are using ANSI SQL to run queries for your analysts. You want to support complex aggregate queries and reuse existing code. How should you store and transform the input data?**

- Use BigQuery for storage. Use Cloud Dataproc to run the transformations.

**5. What will happen to your data in a Bigtable instance if a node goes down?**

- Nothing, as the storage is separated from the node compute

**6. Your company needs to run analytics on their incoming inventory data. They need to use their existing Hadoop workloads to perform this task. What two steps must be performed to accomplish this? (Choose two answers)**

- Stream from Cloud Pub/Sub into Cloud Dataproc, which can then place relevant data in the appropriate storage $ Correct location
- Connect Cloud Dataproc to Bigtable and Cloud Storage, running analytics on the data in both services.

**7. Your company's Kafka server cluster has been unable to scale to the demands of their data ingest needs. Streaming data ingest comes from locations all around the world. How can they migrate this functionality to Google Cloud to be able to scale for future growth?**

- Create a single Pub/Sub topic. Configure endpoints to publish to the Pub/Sub topic, and configure Cloud Dataflow to subscribe to the same topic to process messages as they come in.

**8. You have a long-running, streaming Dataflow pipeline that you need to shut down. You do not need to preserve data currently in the processing pipeline and need it shut down as soon as possible. Which shutdown option should you use to complete the shutdown process?**

- Cancel

**9. Your organization has migrated their Hadoop workloads to Cloud Dataproc. To fully take advantage of the cloud, you want to decouple your Hadoop storage and compute, and be able to destroy your cluster when compute is complete in order to save costs while preserving your data. What should you do?**

- Copy your data from HDFS to Cloud Storage. Update your scripts to point to the Cloud Storage location (gs://) instead of the HDFS location (hdfs://). Within your Dataproc job, configure output to output to Cloud Storage.

**10. You are building a data pipeline on Google Cloud. You need to select services that will host a deep neural network machine learning model also hosted on Google Cloud. You also need to monitor and run jobs that could occasionally fail. What should you do?**

- Use the Cloud Machine Learning Engine to host your model. Monitor the status of the Jobs object for 'failed' job states. 

**11. Your company is making the move to Google Cloud and has chosen to use a managed database service to reduce overhead. Your existing database is used for a product catalog that provides real- time inventory tracking for a retailer. Your database is 500 GB in size. The data is semi-structured and does not need full atomicity. You are looking for a truly no-ops/serverless solution. What storage option should you choose?**

- Cloud Datastore

**12. You are creating a machine learning model to predict the likelihood of fraud from credit card transaction data. The end result will be predicting the percent confidence of two results: "Fraud" and "Not Fraud". What type of learning model problem is this?**

- Classification: categorical is for a set of finite categories, such as 'yes' or 'no'. Fraud is a yes/no output, so this fits. 

**13. You are a consultant for several organizations. Each organization has data in their own BigQuery table within a single project. For application access reasons, all of the tables must remain in the same project. You want to give access to each organization to view and run queries against their own data without exposing the data of organizations to unauthorized viewers. What should you do?**

- Create a separate dataset for each organization in the same project. Place each organization's table in each dataset. Restrict access to the organization's dataset to only that company, from which they can view their table but no one else's: *You can assign roles at the dataset level. Placing tables in different datasets allows you to limit access per dataset.*
- ~~Place all data in a single table, create authorized views restricting access by row based on the SESSION_USER() field. Add that same SESSION_USER() field with the same email addresses according to which company needs access to which roles.~~: *This might technically work, but is substantially more cumbersome than placing each table in a different dataset and is much more prone to error.*

**14. How can you set up your Dataproc environment to use BigQuery as an input and output source?**

- Install the BigQuery connector on your Dataproc cluster

**15. You are training a machine learning model to predict the liklihood of rain based on an available dataset of weather data. In reviewing your input data, the amount of humidity in the air has a very strong influence on the chance of rain, especially compared to less relevant data. How can you incorporate this more important data to that it properly influences the model?**

- Create a feature from the humidity data point, and use L1 regularization to optimize the model.

**16. You currently have a Bigtable instance you've been using for development running a development instance type, using HDD's for storage. You are ready to upgrade your development instance to a production instance for increased performance. You also want to upgrade your storage to SSD's as you need maximum performance for your instance. What should you do?**

- Export your Bigtable data into a new instance, and configure the new instance type as production with SSD's: *Since you cannot change the disk type on an existing Bigtable instance, you will need to export/import your Bigtable data into a new instance with the different storage type. You will need to export to Cloud Storage then back*

**17. As part of a complex rollout, you have hired a third party developer consultant to assist with creating your Dataflow processing pipeline. The data that this pipeline will process is very confidential, and the consultant cannot be allowed to view the data itself. What actions should you take so that they have the ability to help build the pipeline but cannot see the data it will process?**

- Assign the consultant the Dataflow Developer IAM role: *With the Developer IAM role, the developer will be able to create and cancel Dataflow jobs. Without other Google Cloud IAM roles, they will not be able to view the data that will be going through the pipeline.*

**18. When training a machine learning model on AI Platform on a distributed scaled tier, what types of machines are part of that distributed resource?**

- Worker, Master and Parameter server

**19. Which of these is NOT a valid reason to choose an HDD storage type over SSD in a Bigtable instance?**

- You need to maintain costs.
- You plan on running batch workloads instead of frequently executing random reads across a small number of rows
- ~~You need to integrate Bigtable with Cloud Storage~~
- You need to store over 10TB of data.

**20. You are creating a machine learning model for predicting a person's income given a variety of factors such as age, race, occupation, and others. What type of problem are we trying to solve in our prediction values?**

- Linear Regression: *A linear regression problem is a set of continuous values, such as income, stock prices, etc. By contrast, a logistic regression model is more similar to a classification model (yes/no, true/false, etc).*

**21. Your BigQuery table needs to be accessed by team members who are not proficient in technology. You want to simplify the columns they need to query to avoid confusion. How can you do this while preserving all of the data in your table?**

- Create a query that uses the reduced number of columns they will access. Save this query as a view in a different dataset. Give your team members access to the new dataset and instruct them to query against the saved
view instead of the main table.

**22. What is the purpose of hyperparameters in a machine learning training model?**

- Hyperparameters adjust the training process itself: *Learning rate and hidden layers (hyperparameters) are variables that adjust the learning model but have no relation to the training data used.* 

**23. You have 250,000 devices which produce a JSON device status event every 10 seconds. You want to capture this event data for outlier time series analysis. What should you do?**

- Ship the data into Cloud Bigtable. Use the Cloud Bigtable cbt tool to display device outlier data based on your business requirements.

**24. Your online shopping company needs to know when a user has not interacted with the site in 30 minutes. They need the website to alert the user once they have been idle for too long. You use Cloud Dataflow to process the interaction events and decide if an alert should be sent. How should you design the pipeline?**

- Implement a session window with a gap time duration of 30 minutes: *You need a window to be based around the last activity event, which a session window provides.*

**25. You have hundreds of IoT devices that generate 1 TB of streaming data per day. Due to latency, messages will often be delayed compared to when they were generated. You must be able to account for data arriving late within your processing pipeline. What should you do?**

- Enable your IoT devices to generate a timestamp when sending messages. Use Cloud Dataflow to process messages, and use windows, watermarks (timestamp), and triggers to process late data.

**26. Triggers that applies to Dataflow**

- Element count, Combinations of other triggers and Timestamp, ... but not Element size in bytes. 