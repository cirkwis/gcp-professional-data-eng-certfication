# Google Cloud Data Engineer - Final Exam - Attempts 1
**1. You are building a data pipeline on GCP. You need to select services that will host a deep neural network machine learning model also hosted on GCP. You also need to monitor and run jobs that could occasionally fail. What should you do?**
- Use the Cloud Machine Learning Engine to host your model. Monitor the status of the Jobs object for "failed" job states. 

**2. You are designing storage for event data as part of building a data pipeline on GCP. Your input data is in CSV format. You want to minimize the cost of querying individual values over time windows. Which storage service and schema design should you use?**
- Use Cloud Bigtable for storage. Design tall and narrow tables, and use a new row for each single event version. 

**3. How can you setup your Dataproc environment to use BigQuery as an input and output source?**
- Install the BigQuery connector on your Dataproc cluster. 

**4. What is the difference between a deep and wide neural network? What would you use a deep AND wide neural network for?**
- Wide models are used for memorization. Deep models are generalization. 

**5. You need to run analytics queries using SQL syntax against data formatted in JSON format. What should you do?**
- Import the data in JSON format into BigQuery as a table, and run queries against it. 

**6. You are configuring your Cloud Pub/Sub subcription. Assuming that all requirements are met, which subcription delivery method offers better 'near real-time' delivery of messages?**
- Push

**7. You want to export your Cloud SQL Tables into BigQuery for analysis. How can you do this?**
- Export your Cloud SQL data to Cloud Storage, then import into BigQuery

**8. You are setting up Cloud Dataproc to perform some data transformations using Apache Spark jobs. The data will be used for a new set of non-critical experimentations in your marketing group. You want to setup a cluster that can transform a large amount of data in the most cost-effective way. What should you do?**
- **Best choice:** Setup a cluster in Standard mode with high memory machine type. Add 10 additional Preemptible worker nodes. 

**9. Your organisation needs to be able to reliably handle ever-increasing amounts of streaming telemetry data, process it, and economically store analyzed data. What services they can use for this task?**
- Cloud Pub/Sub, Cloud DataFlow, BigQuery

**10. You are migrating a Hadoop cluster to Cloud Dataproc using GCS for storage. After migration, some of your existing, more complex Spark jobs (in parquet format) are performing noticably worse than your on-premise cluster. You are using mostly pre-emptible VM's (with a few required non-preemptible) in order to save on costs.**
- Switch disks from HDD to SSD. Change the default pre-emptible VM settings to inscrease the size of the boot disk. 
  
*By default, preemptible node disk sizes are limited to 100GB or the size of the non-preemptible node disk sizes, whichever is smaller. However you can override the default preemptible disk size to any requested size. Since the majority of our cluster is using preemptible nodes, the size of the disk used for caching operations will see a noticeable performance improvement using a larger disk. Also, SSD's will perform better than HDD. This will increase costs sightly, but is the best option available while maintaining costs and performance.*

- ~~Ensure that your parquet files are at an optimized block size~~

*While the block size of parquet files does have an impact on performance in a complex Spark job, these are the same jobs and configurations that were run on the on-premises Hadoop cluster. The change in performance in two different environments with identical job configurations does not indicate a job configuration or file format issue.*

**11. You are creating a machine learning model for predicting a person's income given a variety of factors such as age, race, occupation and others. What type of problem are we trying to solve in our prediction values?**

- Linear Regression

**12. What is the recommended minimum amount of data to store in BigTable?**

- 1TB: Google recommends that workloads of less than 1TB should not be used in Bigtable, especially form a cost/value perspective. 

**13. You need to choose a structure storage option for storing very large amounts of data with the following properties and requirements:**
- The data has a single key
- You need very low latency
  
**Which solution shoud you choose?**

- Bigtable: *Bigtable uses a single key and has very low latency (in miliseconds)*
- ~~Datastore~~: Datastore stores less data than Bigtable and operates on multiple keys. 

**14. You need to replicate the logs that are ingested by your on-premise Apache Kafka cluster to Google Cloud to be stored for analysis in BigQuery. What should you do?**

- Configure the PubSub Kafka connector on your on-premises Kafka cluster, and configure Pub/Sub as a sink connector. Use a Cloud Dataflow job to read from a subscribed Pub/Sub topic and write to BigQuery. 

**15. You have a Dataflow job that keeps failing due to errors in your input data. What steps can you take to improve pipeline reliability while at the same time, capturing failed data for reprocessing?**

- Implement a try-catch block that transforms the both good and bad data. Create an additional output to use a new PCollection that can be output to Pub/Sub for later analysis.
*Your pipeline needs to use an additional side output, that uses a PCollection to output errorenous data to Pub/Sub*
- ~~Implement a try-catch block that transforms the both good and bad data. Publish the erroneous data to Pub/Sub, which can then be placed inot GCS for further analysis.~~: *Almost correct, however the erroneous data needs to be exported via a side output via PCollection, not just written directly PubSub.* 