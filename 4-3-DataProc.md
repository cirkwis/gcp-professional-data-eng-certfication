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

# Configure Dataproc Cluster and Submit Job
## Create cluster
- gcloud dataproc cluster create [cluster_name] --zone [zone_name]
- Configure master node, worker nodes
  - Master contains YARN resource manager
- Example of creating a Dataproc Cluster via command line: 
```shell
gcloud dataproc clusters create cluster-1 \
--subnet default \
--zone us-central1-b \
--master-machine-type n1-standard-1 \
--master-boot-disk-size 500 \
--num-workers 2 \
--workers-machine-type n1-standard-1 \
--worker-boot-disk-size 500 \
--project pw-data-engineer \
--initialization-actions 'gs://dataproc-initialization-actions/kafka/kafka.sh'
```
- Google-provided Dataproc initialization scripts: https://console.cloud.google.com/storage/browser/dataproc-initialization-actions/ 
- Reference for example job submission: https://cloud.google.com/dataproc/docs/quickstarts/quickstart-console

## Updating clusters 
- Can only change # workers/pre-emptible VM's/labels/toggle gracfull decommission
- Automatically reshards data for you

### Pre-emptible VM"s on Dataproc
- Excellent low cost worker nodes 
- Dataproc manages entire leavejoin process
  - No need to configure startup/shutdown scripts 
  - Just add PVM's... and that's it
- No assigned disks for HDFS (only disk for caching)
- Want a mix of standard + PVM worker nodes
  
## Access your cluster
- SSH into master - same as any computeur engine instance
- gcloud compute ssh [master-node-name]
### Access via web - 2 options
- Open firewall ports to your network (8088, 9870)
- Use SOCKS proxy - does not expose firewall ports
#### SOCKS proxy configuration
- SSH to master to enable port forwarding
  ```shell
  gcloud compute ssh [master-host-name] --project=[project-id] --zone=[master-host-zone] -- -D 1080 -N
  ```