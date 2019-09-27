**What is the HBase Shell for Cloud Bigtable?**

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

