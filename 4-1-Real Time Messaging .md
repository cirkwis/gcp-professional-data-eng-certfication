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
