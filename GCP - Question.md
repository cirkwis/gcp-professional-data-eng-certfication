**1. A multi-national company wants to unify their data sources by building a universal centralized data warehouse instead of their current architecture in which every branch has its own and branches from other regions cannot access it. They want to build a data analytics team to extract data from all branches and build daily reports and dashboards to visualize the metrics required for C-Level managers to take decisions. The current data warehouses are all MySQL databases and analytics team will use SQL for data reporting. The company is distributed among different continents ( North America, Europe &amp; Asia). Which of the following approach is best suits to satisfy the company’s new data warehouse architecture?**

<ol type="A">
  <li>Use Cloud SQL to launch MySQL databases on each region. Enable cross-region read replication for each to sync between different regions.</li>
  <li>Use Cloud SQL to launch Multi-regional MySQL databases. Each in North America, Europe and Asia. Enable cross-region read replication for each to sync between different regions.</li>
  <li>Use BigQuery as a data warehouse and grant data analytics team editor roles.</li>
  <li>Use Cloud Spanner by launching a multi-regional database to be the company’s unified data warehouse.</li>
</ol>

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

<ol type="A">
  <li>Use AutoML Vision to build and train the model by using all the training photos you collected from food-chain’s social media pages for better results.</li>
  <li>Use AutoML Vision to build and train the model by using 50-70% of training photos you collected from food-chain’s social media pages while the rest of training set is to test and tune the model.</li>
  <li>Use Dataproc to build the model using SparkML. Use 50-70% of training photos you collected to train the model and the rest to test and tune the model. Deploy the model using Cloud ML Engine.</li>
  <li>Use Cloud ML Engine with TensorFlow to build the model. Use all training photos you collected to train the model. Deploy the model using Cloud ML Engine.</li>
</ol>

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

**3. A financial services firm providing products such as credit cards and bank loans receives thousands of online applications from clients applying for their products. Because it takes a lot of effort to scan and check all applications if they meet the minimum requirements for the products they are applying for, they want to build a machine learning model takes application fields like annual income, marital status, date of birth, occupation and other attributes as input and finds out if the applicant is qualified for the product the client applied for. Which of the following the machine learning technique will help to build such model?**

<ol type="A">
  <li>Regression</li>
  <li>Classification</li>
  <li>Clustering</li>
  <li>Reinforcement learning</li>
</ol>

>**The correct answer is Option B.**
>
>**A regression problem** is a problem which its output variable is of continuous value. Problems which finds out about variables such as weights, prices or age are considered regression problems. A **classification problem** is a problem which the output variable is a category. Examples of classification problems are finding a passenger’s nationality, detect if a patient is diagnosed with a disease or if an applicant is qualified for a job interview. Regression and classification are supervised learning problems. It means, the machine learns from past experiences by training it on a labeled data set. A training set is a set of rows with input and output parameters. The machine then learns from the training set and improves its parameters for better detection.
>
>**Clustering** is an unsupervised learning method. An unsupervised learning is a method to find references between input data without labeled output. The purpose is to find meaningful structure between the input sets with similar features and group them. Clustering is the method of grouping data points share similarities and separating dissimilar points to other groups. Examples of clustering applications are customer segmentation (new, frequent, loyal, ..), city land value and detecting anomalies in network traffic.
>
>**Reinforcement learning** is a technique which a machine takes actions without training sets to reach the highest rewards possible. The agent learns from trial and decides what to do to perform a given task without supervision. The task punishes the agent for a wrong action and rewards it for achieving the task. Examples of reinforcement learning is asking an agent to play a maze game to reach the exit with traps along the way or making an agent play a video game and win a racing game.
>
>From the explanation above, we can see the scenario problem which finding if a client is qualified for a product is a classification problem. So, option B is correct.

**4. You have built a machine learning model to classify if a customer would buy a certain product when recommended by the company’s website. You trained the model with a sample set. Upon testing the model, you found out only 28% of the testing sets are actually true positives and the model isn’t very accurate. You figured out the model is over-fitted. How would you solve this?**

<ol type="A">
  <li>Increase training data, increase feature parameters &amp; increase regularization.</li>
  <li>Decrease training data, decrease feature parameters &amp; increase regularization.</li>
  <li>Increase training data, decrease feature parameters &amp; increase regularization</li>
  <li>Increase training data, decrease feature parameters &amp; decrease regularization.</li>
</ol>

> **The correct answer is Option C.**
>
> Overfitting happens when a model performs well on a training dataset, generating only a small error, while giving wrong output for the test dataset. This happens because the model is only picking up specific features input found in the training set instead of picking out general features of the given training set.
> To solve overfitting, the following would help improving the model's quality: 
> - Increase the number of examples, the more data a model is trained with, the more use cases the model can be training on and better improves its predictions. 
> - Tune hyperparameters which is related to number and size of hidden layers (for neural networks), and regularization, which means using techniques to make your model simpler such as dropout method to remove neuron networks or adding "penalty" parameters to the cost function.
> - Remove features by removing irrelevant features. Feature engineering is a wide subject and feature selection is a critical part of building and training model. Some algorithms have built-in feature selection, but in some cases, data scientists need to cherry-pick or manually select or remove features for debugging and finding the best model output. 
>
> From the brief explanation, to solve the overfitting problem in the scenario, you need to choose option C. 
  
**5. A coach line bus service company wants to predict how many passengers they expect to book for tickets on their buses for the upcoming months. This helps the company to know how many buses they need to be in service for maintenance and fuel and how many drivers to be available. The company has data sets of all booked tickets since its launch in 1968 and it allows private sharing of the data if this helps the prediction process.**

**You will build the machine learning model for the coach line company. Which technique you will use to predict the number of passengers in the next months?**

<ol type="A">
  <li>Regression</li>
  <li>Association</li>
  <li>Classification</li>
  <li>Clustering</li>
</ol>

>**Answer: A**
>
>A regression problem is a problem which its output variable is of continuous value. Problems which finds out about variables such as weights, prices or age are considered regression problems. A classification problem is a problem which the output variable is a category. Examples of classification problems are finding a passenger’s nationality, detect if a patient is diagnosed with a disease or if an applicant is qualified for a job interview. Regression and classification are supervised learning problems. It means, the machine learns from past experiences by training it on a labeled data set. A training set is a set of rows with input and output parameters. The machine then learns from the training set and improves its parameters for better detection.
>
>Association is a rule-learning technique for discovering interesting relations between variables in large data sets. Example of association rules is discovering regularities between products in large-scale transaction data recorded by point-of-sales for a retail chain store.</p>
>
>Clustering is an unsupervised learning method. An unsupervised learning is a method to find references between input data without labeled output. The purpose is to find meaningful structure between the input sets with similar features and group them. Clustering is the method of grouping data points share similarities and separating dissimilar points to other groups. Examples of clustering applications are customer segmentation (new, frequent, loyal, ..), city land value and detecting anomalies in network traffic.
>
>From the explanation above, the technique to help solving the scenario is Answer A: Regression.

**A video-on-demand company wants to generate subtitles for its content on the web. They have over 20.000 hours of content to be subtitled and their current subtitle team cannot catch up with the every-growing video hours the content team keep adding to the website library. They want a solution to automate this as man power can be expensive and may take long time. Which service of the following can greatly help the automation of video subtitles?**

<ol type="A">
  <li>Cloud Natural Language</li>
  <li>Cloud Speech-to-Text</li>
  <li>AutoML Vision API</li>
  <li>Machine Learning Engine</li>
</ol>

>**Answer: B**
>
<strong>Answer A is incorrect: </strong>Cloud natural language service is to derive insights from unstructured text revealing meaning of the documents and categorize articles. It won’t help extracting captions from videos.</p>

<p><strong>Answer B is correct</strong>: Cloud Speech-to-Text is a service to generate captions from videos by detecting speakers language and speech.</p>

<p><strong>Answer C is incorrect: </strong>AutoML Vision API is a service to recognize and derive insights from images by either using pre-trained models or training a custom model based on a set of photographics.</p>

<p><strong>Answer D is incorrect</strong>: Machine Learning Engine is a managed service letting developers and scientists build their own models and run them in production. This means, you have to build your own model to generate text from videos which needs much effort and experience to build such model. So, it’s not a practical solution for this scenario.</p>

<p><strong>Source(s): </strong></p>

<p>Google NLP: <a href="https://cloud.google.com/natural-language/" target="_blank">https://cloud.google.com/natural-language/</a></p>

<p>Google Machine Learning Engine: <a href="https://cloud.google.com/ml-engine/" target="_blank">https://cloud.google.com/ml-engine/</a></p>

<p>Google Vision API: <a href="https://cloud.google.com/vision" target="_blank">https://cloud.google.com/vision</a></p>

<p>Google Speech-to-Text API: <a href="https://cloud.google.com/speech-to-text/" target="_blank">https://cloud.google.com/speech-to-text/</a></p>
                        </div>

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
