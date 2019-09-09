**16. You work at very large organizations that has a very large analyst team. You use the default pricing model for BigQuery. During heavy usage, your analyst group occasionally runs out of the 2000 slots available for the BigQuery jobs. You do not want to create additional projects for the sole purpose of inscreasing slot count. What can you do to resolve this problem?**

- Switch to flat rate pricing to enable a higher total slot quota for your project. 

**17. You are selecting a streaming service for log messages that must include final result message ordering as part of building a data pipeline on Google Cloud. You want to stream input for 5 days and be able to query the most recent message value. You will be storing the data in a searchable repository. How should you set up the input messages?**

- Use Cloud Pub/Sub for input. Attach a timestamp to every message in the publisher.

**18. You need to deploy a TensorFlow machine-learning model to Google Cloud. You want to maximize the speed and minimize the cost of model prediction and deployment. What should you do?**

- Export your trained model to a SavedModel format. Deploy and run your model on Cloud ML Engine.

**19. Your organization has migrated their Hadoop workloads to Cloud Dataproc. To fully take advantage of the cloud, you want to decouple your Hadoop storage and compute, and be able to destroy your cluster when compute is complete in order to save costs while preserving your data. What should you do?**

- Copy your data from HDFS to Cloud Storage. Update your scripts to point to the Cloud Storage location (gs://) instead of the HDFS location (hdfs://). Within your Dataproc job, configure output to output to Cloud Storage.

**20. Your organization needs to develop their machine learning model to control topology definitions. There are a large number of possible configurations to achieve the best results. What components of their machine learning model would they adjust to account for increased complexity?**

- Neurons: Adding additional neurons allows combining more input values.
- Hidden layers

**21. Your company’s aging Hadoop servers are nearing end of life. Instead of replacing your hardware, your CIO has decided to migrate the cluster to Google Cloud Dataproc. A direct lift and shift migration of the cluster would require 30 TB of disk space per individual node. There are cost concerns about using that much storage. How can you best minimize the cost of the migration?**

- Decouple storage from computer by placing the data in Cloud Storage: Placing all input and output data in Cloud Storage allows you to 
    1. Treat clusters as ephemeral and 
    2. Use a much cheaper storage location compared to persistent disks without a noticeable impact on performance.
- ~~Place archived data in Cloud Storage, and only use 'hot' data in HDFS on the cluster disks.~~: This is technically possible, but all data (hot and cold) can be placed in Cloud Storage and still perform well.

**22. You are setting up multiple MySQL databases on Compute Engine. You need to collect logs from your MySQL applications for audit purposes. How should you approach this?**

- Install the Stackdriver Logging agent on your database instances and configure the fluentd plugin to read and export your MySQL logs into Stackdriver Logging

**23. Your organization is ready to migrate their Hadoop workloads to Google Cloud. For the data migration, they need a cost-effective 'data lake' that will scale to their growing data needs and be able to easily connect to their Hadoop workloads in the cloud. What two actions should they perform?**

- Add the Cloud Storage connector to their on-premises Hadoop environment, and transfer their data to a Cloud Storage bucket.
- For the existing Hadoop jobs that are migrating to Dataproc, use the gs:// prefix instead of hdfs:// to access data from Cloud Storage.

**24. You are working on a project with two compliance requirements. The first requirement states that your developers should be able to see the Google Cloud Platform billing charges for only their projects. The second requirement states that your finance team members can set budgets and view the current charges for all projects in the organization. The finance team should not be able to view the project contents. You want to set permissions. What should you do?**

- Add the finance team members to the Billing Administrator role for each of the billing accounts that they need to manage. Add the developers to the Viewer role for the Project.

**25. You regularly use prefetch caching with a Data Studio report to visualize the results of BigQuery queries. You want to minimize service costs. What should you do?**

- Set up the report to use the Owner's credentials to access the underlying data in BigQuery, and verify that the Enable cache checkbox is selected for the report.

**26. You are training a machine learning model to predict the liklihood of rain based on an available dataset of weather data. In reviewing your input data, the amount of humidity in the air has a very strong influence on the chance of rain, especially compared to less relevant data. How can you incorporate this more important data to that it properly influences the model?**

- Create a feature from the humidity data point, and use L1 regularization to optimize the model: L1 regularization is able to reduce the weights of less important features to zero or near zero.

**27. Your organization is making the move to Google Cloud. You need to bring your existing big data processing workflows to the cloud without having to re-train employees on new products. Your organization uses the Apache Hadoop ecosystem for big data processing. Which Google Cloud managed service would your workflow move to?**

- Cloud Dataproc

**28. In order to protect live customer data, your organization needs to maintain separate operating environments —development/test, staging, and production— to meet the needs of running experiments, deploying new features, and serving production customers. What is the best practice for isolating these environments while at the same time maintaining operability?**

- Create a separate project for dev/test, staging, and production. Migrate relevant data between projects when ready for the next stage.

**29. You want to display aggregate view counts for your YouTube channel data in Data Studio. You want to see the video tiles and view counts summarized over the last 30 days. You also want to segment the data by the Country Code using the fewest possible steps. What should you do?**

- Set up a YouTube data source for your channel data for Data Studio. Set Views as the metric and set Video Title and Country Code as report dimensions. *There is no need to export; you can use the existing YouTube data source. Country Code is a dimension because it's a string and should be displayed as such, that is, showing all countries, instead of filtering.*

**30. Your BigQuery dataset contains 1500 tables. When conducting a query, you are limited to a maximum of 1000 tables that you can query at once. You need to query data across all 1500 tables. What should you do?**

- If possible, merge the 1500 tables to bring the total number below 1000. You may still partition single tables to divide data for queries. *If you have over 1000 tables, you need to bring that number to below 1000 to query all of them at once. Merge tables, then use table partitioning to divide single tables into segments (called partitions), as long they are partitioned by time.*
- ~~Create multiple views of chunks of the 1500 tables, then query the multiple views~~: *This will not work as it will still limit to 1000 tables per query, even if hidden behind views.*

**31. You are building a data pipeline on Google Cloud. You need to prepare source data for a machinelearning model. This involves quickly deduplicating rows from three input tables and also removing outliers from data columns where you do not know the data distribution. What should you do?**

- Use Cloud Dataprep to preview the data distributions in sample source data table columns. Click on each column name, click on each appropriate suggested transformation, and then click Add to add each transformation to the Cloud Dataprep job.

**32. Types of trigger that applies to Dataflow?**

- Element count, Combinations of other triggers, Timestamp
- Element size in bytes is not a type of triggers

**33. What types of Bigtable row keys can lead to hotspotting?**

- Leading with a non-reversed timestamp
- Standard domain names (non-reversed).

*Rows in HBase are sorted lexicographically by row key. This design optimizes for scans, allowing you to store related rows, or rows that will be read together, near each other. However, poorly designed row keys are a common source of hotspotting. Hotspotting occurs when a large amount of client traffic is directed at one node, or only a few nodes, of a cluster. This traffic may represent reads, writes, or other operations. The traffic overwhelms the single machine responsible for hosting that region, causing performance degradation and potentially leading to region unavailability. This can also have adverse effects on other regions hosted by the same region server as that host is unable to service the requested load. It is important to design data access patterns such that the cluster is fully and evenly utilized.*

**34. Some reason to choose an HDD storage type over SSD in a BigTable**

- You need to maintain costs.
- You plan on running batch workloads instead of frequently executing random reads across a small number of rows.
- You need to store over 10TB of data.

**35. Your organization is streaming telemetry data into BigQuery for long-term storage (2 years) and analysis, at the rate of about 100 million records per day. They need to be able to run queries against certain time periods of data without incurring the costs of querying all available records. What is the preferred method for doing so?**

- Partition a single table by day, and run queries against individual partitions.

**36. You created a job which runs daily to import highly sensitive data from an on-premises location to Cloud Storage. You also set up a streaming data insert into Cloud Storage via a Kafka node that is running on a Compute Engine instance. You need to encrypt the data at rest and supply your own encryption key. Your key should not be stored in the Google Cloud. What should you do?**

- Supply your own encryption key, and reference it as part of your API service calls to encrypt your data in Cloud Storage and your Kafka node hosted on Compute Engine.

**37. You have in your possession a database of financial transactions, which include a user's name, location, purchase location, and purchase amount. With this data, what two types of machine learning can potentially applied to this dataset?**

- Unsupervised learning to identify patterns (clustering) in the data to predict the location of future purchases.
- Apply labels to the data based on whether it is fraudulent or not-fraudulent. Then apply supervised classification learning to predict which future transactions are likely to be fraudulent

**38. What open source software is Cloud Pub/Sub most similar to?**

- Kafka

**39. What will happen to your data in a Bigtable instance if a node goes down?**

- Nothing, as the storage is separated from the node compute.

**40. You are a consultant for several organizations. Each organization has data in their own BigQuery table within a single project. For application access reasons, all of the tables must remain in the same project. You want to give access to each organization to view and run queries against their own data without exposing the data of organizations to unauthorized viewers. What should you do?**

- Create a separate dataset for each organization in the same project. Place each organization's table in each dataset. Restrict access to the organization's dataset to only that company, from which they can view their table but no one else's

**41. Two benefits of using denormalized data in BigQuery?**

- Decreased query complexity
- Increased query performance

**42. Your infrastructure runs on another cloud and includes a set of multi-TB enterprise databases that are backed up nightly both on-premises and also to that cloud. You need to create a redundant backup to Google Cloud. You are responsible for performing scheduled monthly disaster recovery drills. You want to create a cost-effective solution. What should you do?**

- Use Storage Transfer Service to transfer the offsite backup files to a Cloud Storage Nearline storage bucket as a final destination: *This is correct because you will need to access your backup data monthly to test your disaster recovery process, so you should use a Nearline bucket; also, because you will be performing ongoing, regular data transfers, so you should use the storage transfer service*
- ~~Use Transfer Appliance to transfer the offsite backup files to a Cloud Storage Coldline bucket as a final
destination.~~: *Transfer Appliance is used for on-premises transfers, not cloud-to-cloud, and is not used for repeated/scheduled transfers. Also, Coldline buckets need to stay un-modified for 3 months (90 days) to avoid additional charges, and your scenario calls for once a month access.*

**43. Your team has decided to use Datalab for interactive machine learning exercises. You want your team members to share their work and progress with each other. How do you accomplish this?**

- Every team member will use their own Datalab notebook and synchronize changes to the shared Cloud Source Repository.