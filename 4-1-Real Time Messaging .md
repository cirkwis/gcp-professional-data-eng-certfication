# Architecture: Real Time Messaging with Cloud Pub/Sub

In this part, we will cover the challenges associated with reliably capturing streaming data, tightly vs. loosely coupled systems, and how Cloud Pub/Sub helps to resolve this issue.

## Streaming Data Challenges

- What is streaming data
  - "Unbounded" data
  - Infinitie, never completes, always flowing
  - Ex: Traffic sensors, Credit Card Transactions, Mobile Gaming
- Fast action is often necessary
  - Must quickly collect data, gain insights and take action
  - Sending to storage can add latency
  - Credit card fraud
  - Predict highway traffic
- Tight vs loosely coupled systems
  - Tightly (direct) coupled systems more likely to fail
  - Loosely coupled systems with "buffer" scale with better fault tolerance

  ![Tight vs loosely coupled systems](./image/4-1.jpg "Tight vs loosely coupled systems")

## Cloud Pub/Sub Overview

We are now going to take a detailed look at what exactly Pub/Sub does, how the process of publishing and subscribing to topics work, and many other points necessary for a thorough understanding. 

### What is Cloud Pub/Sub?
- Global-scale messaging buffer/coupler
- No-ops, global availability, auto-scaling
- Decouples senders and receivers
- Streaming data ingest
  - Also connects other data pipeline services
- Equivalent to Apache Kafka (open source)
- Guaranteed at-least-one delivery
- Asynchronouse messaging - many to many (or any other combination)

 ![Tight vs loosely coupled systems](./image/4-2.jpg "Tight vs loosely coupled systems")

### How it works - terminology?

  ![How it works - terminology?](./image/4-3.jpg "How it works - terminology?")

### Push and Pull
- Pub/Sub can either **push** messages to subcribers, or subscribers can **pull** messages from Pub/Sub;
- Push = lower latency, more real-time
- Push subcribers must be Webhook endpoints that accept POST over HTTPS
- Pull ideal for large volumne of messages - batch delivery

### IAM
- Control access at project, topic, or subscription level
- Admin, Editor, Publisher, Subscriber
- Service accounts are best practice

### Pricing
- Data volumne used per month (per GB)

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-amwm{font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-amwm">Monthly data</th>
    <th class="tg-amwm">Price Per GB</th>
  </tr>
  <tr>
    <td class="tg-0lax">First 10 GB</td>
    <td class="tg-0lax">$0.00</td>
  </tr>
  <tr>
    <td class="tg-0lax">Next 50 TB</td>
    <td class="tg-0lax">$0.06</td>
  </tr>
  <tr>
    <td class="tg-0lax">Next 100 TB</td>
    <td class="tg-0lax">$0.05</td>
  </tr>
  <tr>
    <td class="tg-0lax">Beyond 150 TB</td>
    <td class="tg-0lax">$0.04</td>
  </tr>
</table>

### Out of order messaging
- Messages may arrive from multiple sources out of order
- Pub/Sub does not care about message ordering
- Dataflow is where out of order messages are processed/resolved
- Can add message attributes to help with ordering

Streaming data ingest - GCP 

![Streaming data ingest](./image/4-4.jpg "Streaming data ingest")

##  Pub/Sub Hands On
1. Create a topic called my-topic
```shell
gcloud pubsub topics create my-topic
```
2. Create a subscription to topic my-topic
```shell
gcloud pubsub subscriptions create --topic my-topic mySub1
```
3. Publish a message to topic my-topic
```shell
gcloud pubsub topics publish my-topic --message "Hello"
```
4. Retrieve message with your subscription, acknowledge receipt and remove message from the queue
```shell
gcloud pubsub subscriptions pull --auto-ack mySub1
```
5. Cancel subscription
```shell
gcloud pubsub subscriptions delete mySub1
```

## Example use case
1. Simulated traffic ingest:
Clone GitHub data to Cloud Shell (or other SDK environments), and browse to the publish folder:
```shell
cd ~ git clone https://github.com/linuxacademy/googledataengineer
cd ~/googledataengineer/courses/streaming/publish
```
2. Create a topic called sandiego:
```shell
gcloud pubsub topics create sandiego
```
3. Create a subscription to topic sandiego:
```shell
gcloud pubsub subscriptions create --topic sandiego mySub1
```
4. Run script to download sensor data:
```shell
./download_data.sh
```
(Optional). If you need to authenticate a shell to ensure we have the right permissions:
```shell
gcloud auth application-default login
```
5. View script info:
```shell
vim ./send_sensor_data.py 
```
6. Run python script to simulate one hour of data per minute:
```shell
./send_sensor_data.py --speedFactor=60 --project=$PROJECT_ID
```
If you receive an error: google.cloud.pubsub cannot be found OR ‘ImportError: No module named iterator’, run the below pip command to install components then try again:
```shell
sudo pip install -U google-cloud-pubsub
```
7. Open new Cloud Shell tab (using + symbol) and Pull the message using the subscription mySub1
```shell
gcloud pubsub subscriptions pull --auto-ack mySub1
```

8. Create a new subscription and pull messages with it:

```shell
gcloud pubsub subscriptions create --topic sandiego mySub2
gcloud pubsub subscriptions pull --auto-ack mySub2
```

## Connecting Kafka to GCP
Existing on premises workloads may need to use an existing Apache Kafka cluster to connect to GCP. This part covers the basics of how to integrate Kafka with GCP, focusing on how connectors work.

[Kafka connectors for GCP](https://cloud.google.com/blog/products/gcp/apache-kafka-for-gcp-users-connectors-for-pubsub-dataflow-and-bigquery)

### Does Pub/Sub replace Kafka?
- Not always
- Hybrid workload:
  - Interact with existing tools and frameworks
  - Don't need global/scaling capabilities with Pub/Sub
- Can use both Kafka for on-premise and Pub/Sub for GCP in the same data pipeline

### How to connect Kafka to GCP
![How to connect Kafka to GCP](./image/4-5.jpg "How to connect Kafka to GCP")
- Connectors!
  - Open source plug-ins that connect Kafka to GCP
  - Kafka Connect - optional "connector service"
  - Connectors exist to connect Kafka directly to PubSub, Dataflow and BigQuery (among others)
- Terminology - Source and Sink connectors
  - **Source connector** - Upstream connector: Stream from something to Kafka 
  - **Sink connector** - Downstream connector: Stream from Kafka to something else

  

## Monitoring Subscriber Health

### In a perfect world...
- Subscribers and Publishers in perfect harmony
- Example:
  - 1 million messages/second published
  - 1 million messages/second successfully pull/pushed
  - Result: No backlog in PubSub queue
- But we don't live in a perfect world: 
  - Subscriber cannot keep up with publish rate
  - Result: Backlog in PubSub queue

### Troubleshooting subsriber health (backlog)
![Troubleshooting subsriber health](./image/4-6.jpg "Troubleshooting subsriber health")
- Create alerts for (x) backlog thresold
- Subscriber not able to keep-up
  - Under-provisioned
  - Code not optimized
- Not acknowledging message receipt 
  - PubSub doesn't know it's delivered - keep trying
  - Subscriber code not properly acknowledging pulled messages
- Check Publishers for excessive re-transmits
  

