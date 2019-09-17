# Google Cloud Data Engineer - Final Exam - Attempts 2

**1. Which of these open source frameworks is best suited to process simultaneous batch and streaming in a single data pipeline?**

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

**27. You are developing an application that will only recognize and tag specific business to business product logos in images. What is the best method to accomplish this task?**

- Create a custom machine learning model to recognize specific logos in photos, then train it on Cloud ML Engine.

**28. You need to replicate the logs that are ingested by your on-premises Apache Kafka cluster to Google Cloud to be stored for analysis in BigQuery. What should you do?**

- Configure the Pub/Sub Kafka connector on your on-premises Kafka cluster, and configure Pub/Sub as a sink connector. Use a Cloud Dataflow job to read from a subscribed Pub/Sub topic and write to BigQuery. 

**29. In machine learning, what is the difference between test and training data?**

- Training data has a label attached to train on features for the correct answer. Test data is used to test the trained model for accuracy when completed on new data.

**30. You are building a data pipeline on Google Cloud. You need to prepare source data for a machinelearning model. This involves quickly deduplicating rows from three input tables and also removing outliers from data columns where you do not know the data distribution. What should you do?**

- Use Cloud Dataprep to preview the data distributions in sample source data table columns. Click on each column name, click on each appropriate suggested transformation, and then click Add to add each transformation to the Cloud Dataprep job.

**31. Your company’s aging Hadoop servers are nearing end of life. Instead of replacing your hardware, your CIO has decided to migrate the cluster to Google Cloud Dataproc. A direct lift and shift migration of the cluster would require 30 TB of disk space per individual node. There are cost concerns about using that much storage. How can you best minimize the cost of the migration?**

- Decouple storage from computer by placing the data in Cloud Storage

**32. Your organization needs to be able to reliably handle ever-increasing amounts of streaming telemetry data, process it, and economically store analyzed data. What services should they use for this task?**

- Cloud Pub/Sub, Cloud Dataflow, Bigquery

**33. You are working on a project with two compliance requirements. The first requirement states that your developers should be able to see the Google Cloud Platform billing charges for only their projects. The second requirement states that your finance team members can set budgets and view the current charges for all projects in the organization. The finance team should not be able to view the project contents. You want to set permissions. What should you do?**

- Add the finance team members to the Billing Administrator role for each of the billing accounts that they need to manage. Add the developers to the Viewer role for the Project.

**34. Which of these numbers are adjusted by a machine learning neural network as it works with its training dataset?**

- Weights and Biases

**35. Two benefits of using denormalized data in BigQuery?**

- Decreased query complexity
- Increased query performance

**36. When training a machine learning model, why do you need separate training and test data?**

- Without different data, your model will not generalize for additional data, known as overfitting.

**37. What types of jobs does Cloud Dataproc support?**

- Hive, Pig and Spark, ...

**38. You are training a facial detection machine learning model. Your model is suffering from overfitting your training data. Choose three steps you can take to solve this problem**

- Use a smaller set of features
- Increase the number of training examples
- Increase the regularization parameters

**39. You are selecting a streaming service for log messages that must include final result message ordering as part of building a data pipeline on Google Cloud. You want to stream input for 5 days and be able to query the most recent message value. You will be storing the data in a searchable repository. How should you set up the input messages?**

- Use Cloud Pub/Sub for input. Attach a timestamp to every message in the publisher.

**40. You want to display aggregate view counts for your YouTube channel data in Data Studio. You want to see the video tiles and view counts summarized over the last 30 days. You also want to segment the data by the Country Code using the fewest possible steps. What should you do?**

- Set up a YouTube data source for your channel data for Data Studio. Set Views as the metric and set Video Title and Country Code as report dimensions.

**41. Why do you want to train a machine learning model locally before training on cloud resources**

- Faster iteration.
- Save costs

**42. Your infrastructure includes two 100-TB enterprise file servers. You need to perform a one-way, onetime migration of this data to the Google Cloud securely. Only users in Germany will access this data. You want to create the most cost-effective solution. What should you do?**

- Use Transfer Appliance to transfer the offsite backup files to a Cloud Storage Regional storage bucket as a final destination: *This answer is correct because you are performing a one-time (rather than an ongoing series) data transfer from onpremises to Google Cloud Platform for users in a single region (Germany). Using a Regional storage bucket will reduce cost and also conform to regulatory requirements.*
- ~~Use Storage Transfer Service to transfer the offsite backup files to a Cloud Storage Regional storage bucket as a final destination~~: *Storage Transfer Service is not for data stored on-premises, but for AWS/Google Cloud/online locations.*

**43. As part of your backup plan, you create regular boot-disk snapshots of Compute Engine instances that are running. You want to be able to restore these snapshots using the fewest possible steps for replacement instances. What should you do?**

- Use the snapshots to create replacement instances as needed.

**44. While conducting BigQuery queries against a large table with many columns, you notice in the details section that you have a very large purple bar in the first stage of your query execution. How can you troubleshoot this to increase performance and reduce costs?**

- Restrict the number of columns in your SELECT field for those needed. This will reduce read times on your query: *The purple bar indicates the number of read operations. Limiting columns read will reduce the read time of your query.*
- Partition or separate your large table into smaller pieces. Conduct a query against your smaller (or partitioned) tables to reduce read times.

**45. When using AI Platform to train machine learning models, how are online predictions different from batch predictions?**

- Online predictions are returned in the response message.
- Batch predictions are optimized to handle a high volume of prediction examples while running on more complex models.

**46. You are migrating a Hadoop cluster to Cloud Dataproc using GCS for storage. After migration, some of your existing, more complex Spark jobs (in parquet format) are performing noticably worse than your on-premises cluster. You are using mostly preemptible VM's (with a few required nonpreemptible) in order to save on costs.**

- Switch disks from HDD to SSD. Change the default preemptible VM settings to increase the size of the boot disk: *By default, preemptible node disk sizes are limited to 100GB or the size of the non-preemptible node disk sizes, whichever is smaller. However you can override the default preemptible disk size to any requested size. Since the majority of our cluster is using preemptible nodes, the size of the disk used for caching operations will see a noticeable performance improvement using a larger disk. Also, SSD's will perform better than HDD. This will increase costs slightly, but is the best option available while maintaining costs.*

**47. You are evaluating a storage solution for your data. Your data is in a structured, non-relational format, and will be used for analysis. You need the lowest latency read and write speeds possible. Your data is about 3 TB in size, predicted to grow to up to 5 TB. What solution should you use?**

- Use Cloud Bigtable with SSD storage.

**48. Your organization is streaming telemetry data into BigQuery for long-term storage (2 years) and analysis, at the rate of about 100 million records per day. They need to be able to run queries against certain time periods of data without incurring the costs of querying all available records. What is the preferred method for doing so?**

- Partition a single table by day, and run queries against individual partitions.

**49. You regularly use prefetch caching with a Data Studio report to visualize the results of BigQuery queries. You want to minimize service costs. What should you do?**

- Set up the report to use the Owner's credentials to access the underlying data in BigQuery, and verify that the Enable cache checkbox is selected for the report.

**50. Your organization needs to develop their machine learning model to control topology definitions. There are a large number of possible configurations to achieve the best results. What components of their machine learning model would they adjust to account for increased complexity? (Choose two answers.)**

- Neurons
- Hidden layers