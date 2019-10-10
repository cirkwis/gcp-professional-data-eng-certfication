**1. A multi-national company wants to unify their data sources by building a universal centralized data warehouse instead of their current architecture in which every branch has its own and branches from other regions cannot access it. They want to build a data analytics team to extract data from all branches and build daily reports and dashboards to visualize the metrics required for C-Level managers to take decisions. The current data warehouses are all MySQL databases and analytics team will use SQL for data reporting. The company is distributed among different continents ( North America, Europe &amp; Asia). Which of the following approach is best suits to satisfy the company’s new data warehouse architecture?**

- **A.** Use Cloud SQL to launch MySQL databases on each region. Enable cross-region read replication for each to sync between different regions.
- **B.** Use Cloud SQL to launch Multi-regional MySQL databases. Each in North America, Europe and Asia. Enable cross-region read replication for each to sync between different regions.
- **C.** Use BigQuery as a data warehouse and grant data analytics team editor roles.
- **D.** Use Cloud Spanner by launching a multi-regional database to be the company’s unified data warehouse.

> **The correct answer is Option D**
> 
> Cloud Spanner is a horizontally scalable, strongly consistent, relational database service. It’s built to combine the benefits of relational database structure with non-relational horizontal scale. This delivers high-performance transactions and strong consistency across rows, regions and continents.
> 
> <p><strong>Option A is incorrect.</strong> Launching MySQL databases on each region defeats the purpose of having a unified data warehouse.</p>
> 
> <p><strong>Option B is incorrect</strong>. Cloud SQL does not support multi-regional databases.</p>
> 
> <p><strong>Option C is incorrect</strong>. While BigQuery is a strong and potential alternative, BigQuery does not have horizontal scaling and it only covers USA &amp; Europe (<em>by the time of writing this question</em>). Another drawback is, BigQuery doesn’t support full data manipulation language (DML) and it has limitations on how rows can be updated or deleted.</p>
> 
> <p><strong>Option D is correct.</strong> Cloud Spanner is a relational database supports horizontal scaling across continents.</p>
> 
> <p><strong>Source(s) :</strong><a href="https://cloud.google.com/spanner/" target="_blank">Cloud Spanner</a>, <a href="https://cloud.google.com/bigquery/docs/locations" target="_blank">BigQuery dataset locations</a>, <a href="https://cloud.google.com/bigquery/docs/reference/standard-%20sql/data-manipulation-language" target="_blank">Bigquery: Data Manipulation Langauge</a></p>

**2. A fast-food chain restaurant wants to detect the different meal photos its customers upload to the different social media platforms tagged with their name in order to know what meals customers like and share the most for better quality analysis. It asks your advice on developing such solution for them.**

**However, they want it to be available and in production the soonest possible because they expect a high activity on their social media pages by the next public holiday which is coming in 2 weeks and marketing team finds it a great opportunity to receive feedback based on what customers say online. What is the best approach for this?**

- A. Use AutoML Vision to build and train the model by using all the training photos you collected from food-chain’s social media pages for better results.
- B. Use AutoML Vision to build and train the model by using 50-70% of training photos you collected from food-chain’s social media pages while the rest of training set is to test and tune the model.
- C. Use Dataproc to build the model using SparkML. Use 50-70% of training photos you collected to train the model and the rest to test and tune the model. Deploy the model using Cloud ML Engine.
- D. Use Cloud ML Engine with TensorFlow to build the model. Use all training photos you collected to train the model. Deploy the model using Cloud ML Engine.

>**The correct answer is Option B**
>
>Since you have a very short time to build, train and deploy the model, building your own model can be time-consuming and not in your favor. Google provides a great ML service called AutoML to quickly build models for you. AutoML Vision is one of its products which you can start with a training set as little as a dozen photo samples and AutoML takes care of the rest.
>
><strong>Option A is incorrect</strong>. AutoML Vision is the right choice. However, training the model with whole training set is not the right approach in Machine Learning because you ought to test the model before considering it accurate enough for production. Usually, training set is split into 70-30% sets, first for training while the second is for testing and tuning the model’s parameters.
>
><strong>Option C is incorrect</strong>. Using any approach other than AutoML can be time-consuming and with such tight deadline, it’s not the best approach.
>
><strong>Option D is incorrect</strong>. Using this approach can also be time-consuming and using the whole training set for training is not a best practice as explained before.
>
>Thus, the best approach for this scenario is Option B.
>
><strong>Source(s) :</strong> <a href="https://cloud.google.com/automl/" target="_blank">Google Cloud AutoML</a>, <a href="https://cloud.google.com/ml-engine/" target="_blank">Cloud Machine Learning Engine</a>
  
**1. What is the HBase Shell for Cloud Bigtable?**

- ~~The HBase shell is a GUI based interface that performs administrative tasks, such as creating and deleting tables.~~
- The HBase shell is a command-line tool that performs administrative tasks, such as creating and deleting tables.
- ~~The HBase shell is a hypervisor based shell that performs administrative tasks, such as creating and deleting new virtualized instances.~~
- ~~The HBase shell is a command-line tool that performs only user account management functions to grant access to Cloud Bigtable instances.~~

<div>
The HBase shell is a command-line tool that performs administrative tasks, such as creating and deleting tables. The Cloud Bigtable HBase client for Java makes it possible to use the HBase shell to connect to Cloud Bigtable.

Reference: https://cloud.google.com/bigtable/docs/installing-hbase-shell
</div>

**What is the recommended action to do in order to switch between SSD and HDD storage for your Google Cloud Bigtable instance?**
- ~~create a third instance and sync the data from the two storage types via batch jobs~~
- export the data from the existing instance and import the data into a new instance
- ~~run parallel instances where one is HDD and the other is SDD~~
- ~~the selection is final and you must resume using the same storage type~~

<div>
When you create a Cloud Bigtable instance and cluster, your choice of SSD or HDD storage for the cluster is permanent. You cannot use the Google Cloud
Platform Console to change the type of storage that is used for the cluster.
If you need to convert an existing HDD cluster to SSD, or vice-versa, you can export the data from the existing instance and import the data into a new instance.

Alternatively, you can write - a Cloud Dataflow or Hadoop MapReduce job that copies the data from one instance to another.

Reference: https://cloud.google.com/bigtable/docs/choosing-ssd-hdd
</div>

**Which of the following is NOT a valid use case to select HDD as the storage for GCP Bigtable**
- ~~You expect to store at least 10TB of data~~ 
- ~~You will mostly run batch workloads with scans and writes, rather than frequently executing random reads of a small number of rows~~
- You need to integrate with Google BigQuery
- ~~You will not use the data to back an user-facing or latency-sensitive application~~

<div>
For example, if you plan to store extensive historical data for a large number of remote-sensing devices and then use the data to generate daily reports, the cost savings for HDD storage may justify the performance tradeoff. On the other hand, if you plan to use the data to display a real-time dashboard, it probably would not make sens to use HDD storage, reads would be much more frequent in this case, and reads are much slower with HDD storage. 
</div>

**Cloud Bigtable is Google's NoSQL Big Data database service**

**When you store data in Cloud Bigtable, what is the recommended minimum amount of stored data?**
- 1TB
<div>
Cloud Bigtable is not a relational database; It does not support SQL queries, joins or multi-row transactions. It's not a good solution for less than 1TB of data. 
Ref: https://cloud.google.com/bigtable/docs/overview#title_short_and_other_storage_options
</div>

**If you're running a performance test that depends upon Cloud Bigtable, recommended steps are:**
- Use a production instance: A developpement instance will not give you an accurate sense of how a production instance performs under load. 
- Run your test for at least 10 minutes: This step lets Cloud Bigtable further optimize your data, and it helps ensure  that you will test reads from disk as well as cached reads from memory. 
- Before you test, run a heavy pre-test for several minutes: this step gives Cloud Bigtable a chance to balance data across nodes based on the access patterns it observes. 
- Use at least 300 GB of data: 300 GB of data is enough to provide reasonable results in a performance test on a 3-node cluster. On larger clusters, use 100GB of data per node. 

**Cloud Bigtable is a recommended option for storing very large amounts of:**
- single-keyed data with very low latency

**Which row keys are likely to cause a disproportionate number of reads and/or writes on a particular node in a Bigtable cluster**
- A sequential numeric ID 
- A timestamp followed by a stock symbol
- ~~A non-sequential numeric~~
- ~~A stock symbol followed by a timestamp~~

<div>
...using a timestamp as the first element of a row key can cause a variety of problems. 

In brief, when a row key for a time series includes a timestamp, all of your writes will target a single node; fill that node; and then move onto the next node in the cluster, resulting in hotspotting. Suppose your system assigns a numeric ID to each of your application's users. You might be tempted to use the user's numeric ID as the row key for your table. 
</div>
