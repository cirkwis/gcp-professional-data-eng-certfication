# DataProc overview
## DataProc overview 
### What is Cloud Dataproc?
- Managed version of Hadoop ecosystem
  - Hadoop, Spark, Pig, Hive
  - Lift and Shift to GCP
- Dataproc facts:
  - On-demand, managed Hadoop and Spark clusters
  - Managed, but not no-ops
    - Must configure cluster, not auto-scaling
    - Greatly reduces administrative overhead
  - Integrates with other GCP services
    - Separate data from cluster - save costs
  - Familiar Hadoop/Spark ecosystem environment
    - Easy to move existing projects
  - Base on Apache Bigtop distribution
    - Hadoop, Spark, Hive, Pig
  - HDFS available (but maybe not optimal)
  - Other ecosystem tools can be installed as well via initialization actions
### What is MapReduce?
Simple definition: Take big data, distribute it to many workers (map), combine results of many pieces (reduce)
- Distributed/parallel computing
![What is MapReduce?](./image/4-3-1.png "What is MapReduce?")
###  Pricing
- Standard Compute Engine machine type pricing + managed Dataproc premiumn
- Premiumn = $0.01 per vCPU core/hour. More about pricing https://cloud.google.com/dataproc/pricing 
![Data Lifecyle Scenario](./image/4-3-2.png "Data Lifecyle Scenario")
### IAM - Identity and Access Management
- Project level only (primitive and predefined roles)
- Cloud Dataproc Editor, Viewer, Worker
- **Editor** - Full access to create/delete/edit clusters/job/workflows
- **Viewer** - View access only
- **Worker** - Assigned to service accounts: Read/write GCS, write to Cloud Logging

![Dataflow vs Dataproc? Beam vs Hadoop/Spark?](./image/4-2-4.png "Dataflow vs Dataproc? Beam vs Hadoop/Spark?")