## What's Ahead?
In this lesson, you're going to get familiar with what's meant by machine learning deployment. Then in the upcoming lessons, you will put these ideas to practice by using Amazon's SageMaker. SageMaker is just one method for deploying machine learning models.

Specifically in this lesson, we will look at answering the following questions:

* What's the machine learning workflow?

* How does deployment fit into the machine learning workflow?

* What is cloud computing?

* Why would we use cloud computing for deploying machine learning models?

* Why isn't deployment a part of many machine learning curriculums?

* What does it mean for a model to be deployed?

* What are the essential characteristics associated with the code of deployed models?

> What are different cloud computing platforms we might use to deploy our machine learning models?
At the end of this lesson, you'll understand the broader idea of machine learning deployment. Then Sean will be guiding you through using SageMaker to deploy your own machine learning models. This is a lot to cover, but by the end you will have a general idea of all the concepts related to deploying machine learning models into real world production systems.

## Machine Learning Workflow

### References
Below are links that provide more detailed information on the Machine Learning Workflow that we discussed in this section above, described by cloud providers: Amazon, Google, and Microsoft.

1. Amazon Web Services (AWS) discusses their definition of the [Machine Learning Workflow.](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-mlconcepts.html)

2. Google Cloud Platform (GCP) discusses their definition of the [Machine Learning Workflow.](https://cloud.google.com/ml-engine/docs/tensorflow/ml-solutions-overview)

3. Microsoft Azure (Azure) discusses their definition of the [Machine Learning Workflow.](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml)

## Notes:
All algorithms used within the machine learning workflow are similar for both the cloud and on-premise computing. The only real difference may be in the user interface and libraries that will be used to execute the machine learning workflow.

For personal use, one’s likely to use cloud services, if they don’t have enough computing capacity.

With academic use, quite often one will use the university’s on-premise computing resources, given their availability. For smaller universities or research groups with few funding resources, cloud services might offer a viable alternative to university computing resources.

For workplace usage, the amount of cloud resources used depends upon an organization’s existing infrastructure and their vulnerability to the risks of cloud computing. A workplace may have security concerns, operational governance concerns, and/or compliance and legal concerns regarding cloud usage. Additionally, a workplace may already have on-premise infrastructure that supports the workflow; therefore, making cloud usage an unnecessary expenditure. Keep in mind, many progressive companies may be incorporating cloud computing into their business due to the business drivers and benefits of cloud computing.

## Deployment to Production
Recall that:
Deployment to production can simply be thought of as a method that integrates a machine learning model into an existing production environment so that the model can be used to make decisions or predictions based upon data input into the model.

This means that moving from modeling to deployment, a model needs to be provided to those responsible for deployment. We are going to assume that the machine learning model we will be deploying was developed in Python.

## Paths to Deployment
There are three primary methods used to transfer a model from the modeling component to the deployment component of the machine learning workflow. We will be discussing them in order of least to most commonly used. The third method that's most similar to what’s used for deployment within Amazon’s SageMaker.

#### Paths to Deployment:

* Python model is recoded into the programming language of the production environment.
 
* Model is coded in Predictive Model Markup Language (PMML) or Portable Format Analytics (PFA).
 
* Python model is converted into a format that can be used in the production environment.
 
#### Recoding Model into Programming Language of Production Environment
The first method which involves recoding the Python model into the language of the production environment, often Java or C++. This method is rarely used anymore because it takes time to recode, test, and validate the model that provides the same predictions as the original.

#### Model is Coded in PMML or PFA
The second method is to code the model in Predictive Model Markup Language (PMML) or Portable Format for Analytics (PFA), which are two complementary standards that simplify moving predictive models to deployment into a production environment. The Data Mining Group developed both PMML and PFA to provide vendor-neutral executable model specifications for certain predictive models used by data mining and machine learning. Certain analytic software allows for the direct import of PMML including but not limited to IBM SPSS, R, SAS Base & Enterprise Miner, Apache Spark, Teradata Warehouse Miner, and TIBCO Spotfire.

#### Model is Converted into Format that’s used in the Production Environment
The third method is to build a Python model and use libraries and methods that convert the model into code that can be used in the production environment. Specifically most popular machine learning software frameworks, like PyTorch, TensorFlow, SciKit-Learn, have methods that will convert Python models into intermediate standard format, like ONNX (Open Neural Network Exchange format). This intermediate standard format then can be converted into the software native to the production environment.

* This is the easiest and fastest way to move a Python model from modeling directly to deployment.
* Moving forward this is typically the way models are moved into the production environment.
* Technologies like containers, endpoints, and APIs (Application Programming Interfaces) also help ease the work required for deploying a model into the production environment.

We will discuss these technologies in more detail in the next sections.

### Machine Learning Workflow and DevOps

</br>

<img src="/Visual Representations/mlworkflow-devops.png"/></p>

</br>

#### Machine Learning Workflow and Deployment
Considering the components of the Machine Learning Workflow, one can see how Exploring and Processing Data is tightly coupled with Modeling. The modeling can’t occur without first having the data the model will be based upon prepared for the modeling process.

Comparatively deployment is more tightly coupled with the production environment than with modeling or exploring and processing the data. Therefore, traditionally there’s was a separation between Deployment and the other components of the machine learning workflow. Specifically looking at the diagram above, the Process Data and Modeling are considered Development; whereas, Deployment is typically considered Operations.

In the past typically, development was handled by analysts; whereas, operations was handled by software developers responsible for the production environment. With recent developments in technology (containers, endpoints, APIs) and the most common path of deployment; this division between development and operations softens. The softening of this division enables analysts to handle certain aspects of deployment and enables faster updates to faltering models.

### Deployment within Machine Learning Curriculum
Deployment is not commonly included in machine learning curriculum. This likely is associated with the analyst's typical focus on Exploring and Processing Data and Modeling, and the software developer's focusing more on Deployment and the production environment. Advances in cloud services, like [SageMaker](https://aws.amazon.com/sagemaker/) and [ML Engine](https://cloud.google.com/ml-engine/), and deployment technologies, like Containers and REST APIs, allow for analysts to easily take on the responsibilities of deployment.

## Production Environment and the Endpoint
When we discussed the production environment, the endpoint was defined as the interface to the model. This interface (endpoint) facilitates an ease of communication between the model and the application. Specifically, this interface (endpoint)

* Allows the application to send user data to the model and
* Receives predictions back from the model based upon that user data.

## Model, Application, and Endpoint

---- 

One way to think of the endpoint that acts as this interface, is to think of a Python program where:

* the endpoint itself is like a function call
* the function itself would be the model and
* the Python program is the application.

The image above depicts the association between a Python program and the endpoint, model, and application.

* the endpoint: line 8 function call to ml_model
* the model: beginning on line 14 function definition for ml_model
* the application: Python program web_app.py

----

Using this example above notice the following:

* Similar to a function call the endpoint accepts user data as the input and returns the model’s prediction based upon this input through the endpoint.
* In the example, the user data is the input argument and the prediction is the returned value from the function call.
* The application, here the python program, displays the model’s prediction to the application user.

This example highlights how the endpoint itself is just the interface between the model and the application; where this interface enables users to get predictions from the deployed model based on their user data.

Next we'll focus on how the endpoint (interface) facilitates communication between application and model.

### Endpoint and REST API
Communication between the application and the model is done through the endpoint (interface), where the endpoint is an Application Programming Interface (API).

* An easy way to think of an API, is as a set of rules that enable programs, here the application and the model, to communicate with each other.
* In this case, our API uses a REpresentational State Transfer, REST, architecture that provides a framework for the set of rules and constraints that must be adhered to for communication between programs.
* This REST API is one that uses HTTP requests and responses to enable communication between the application and the model through the endpoint (interface).
* Noting that both the HTTP request and HTTP response are communications sent between the application and model.
The HTTP request that’s sent from your application to your model is composed of four parts:

* Endpoint
This endpoint will be in the form of a URL, Uniform Resource Locator, which is commonly known as a web address.

* HTTP Method
Below you will find four of the HTTP methods, but for purposes of deployment our application will use the POST method only.

* HTTP Headers
The headers will contain additional information, like the format of the data within the message, that’s passed to the receiving program.

* Message (Data or Body)
The final part is the message (data or body); for deployment will contain the user’s data which is input into the model.
