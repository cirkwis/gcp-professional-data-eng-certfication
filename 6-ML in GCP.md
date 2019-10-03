## What is Machine Learning (ML)?
- Machine learning is a way to use standard algorithms to derive predictive insights from data and make repeated decisions.
- backward-looking use of data - looking at historical data to create reports and dashboards
- Question about automating: 
  - make decision for every production in every region?
  - dynamically adjust the price? 
  - make decisions around predictive insights repeatable
- ML is about scaling up BI and decision making

## Stage 1: Train an ML model with examples
- The first stage of ML is to train an ML model with examples. 
- In this section, we focus on supervised learning which starts from examples. 
- An example consists of an input and a label (the true answer of this input). 

## Preventing Overfitted Training Models 

### What is Overfitting?
- Training model "overfitted" to training data - unable to generalize with new data
- Training model "fails to generalize" - account for slightly different but close enough data

### Causes of overfitting
- Not enought training data: Need more variety of samples
- Too many features: too complex
- Model fitted to unnecessary features unique to training data - a.k.a "Noise" 

### Solving for overfitted model
- MORE DATA!
    - Add more training data
    - Better generalize on variety
- Make model less complex
    - Use less (but more relevent) features
    - Combine multiple co-dependant/redundant features into single representative feature: Also helps reduce model training time
- Remove "noise": increase **regularization** parameters

### Regularization
- Adds a penalty to model as model becomes more complex
- Penalizes *parameters* = better generalize
- Cuts out "noise" and unimportant data to avoid overfitting

#### Regularization types: 
- **L1 and L2 regularization** - different approaches to tuning out noise. Each has different use case and purpose. 
- **L1** - Lasso Regression - assigns greater importance to **more influential features**
    - Shrinks less important features influence to zero
    - Good for models with many features, some more important than others
    - Example: Choosing features to predict likehood of home selling => House price more influential feature than carpet color. 
- **L2** - Ridge Regression - performs better when all the input features influence the output and all with weights are of **roughly equal size**

## ML Options on Google Cloud Platform
- Pre-trained ML models
- AI Platform: 
    - Train, deploy and manage custom ML models on managed infrastructure resources
    - You create the model and Google provide managed infrastructure for testing it. 
    - Distributed training and prediction: breaks job down into pieces, distributes to multiple workers
    - Automate the "annoying bits" of machine learning
    - Training automatically the model
![AI Platform](./image/6-2.JPG "AI Platform")

## How AI Platform works:
- Prepare trainer and data for the cloud: 
    - write training application in Tensorflow (or other ML library)
    - Python is language of choice
- Train your model with AI Platform
    - **Master** - manages other nodes
    - **Workers** - works on portion of training job
    - **Parameter servers** - coordinate shared model state between workers 

![AI Platform](./image/6-3.JPG "AI Platform")

## Get Predictions - two types: 
- Online: 
    - High rate of requests with minimal latency
    - Give job data in JSON request string, predictions returned in its response message
- Batch:
    - Get inference (predictions) on large collections of data with minimal job duration
    - Input and output in Cloud Storage

## Key terminology in AI Platform
- Model - logical container individual solutions to a problem: 
    - Can deploy multiple version
- Version - instance of model
- Job - interactions with AI Platform
    - Train models: command = 'submit job train model' on AI Platform
    - Deploy trained models: command = 'submit job deploy trained model' on AI Platform
    - 'Failed' jobs can be monitored for troubleshooting

## Features Engineering: Good features
- Good features bring human insight to problem
- Options for encoding categorical data. These are all different ways to create a SPARSE-column
- Crossing features can simplify learning: crossing two or more feature to make a new feature. 
## Features Engineering: Causuality
- Feature value known at the time prediction is made? 
- Causal: can not realy on future information
- Must ingest that data in timely manner
- Legal/ethical to collect use that information
## Features Engineering: Numeric with meaningful magnitude
- Non-numeric features can be used, it's just that we need to find a way to represent them in numeric form
## Features Engineering: Enough example

## Features Engineering: Bucketizing 
The transformation of numeric features into categorical features, using a set of thresholds, is called bucketing (or binning)

## Features Engineering: Wide and Deep 
- Two types of features: Dense and Sparse
![Dense and Sparse](./image/6-1.JPG "Dense and Sparse")
- DNNs good for dense, higly correlated
- Linear for spare, independent features 
