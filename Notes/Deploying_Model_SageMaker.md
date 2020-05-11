## Deploying a Model in SageMaker

[Deployment](https://youtu.be/g_GYZpcVcFE)

In this lesson, we're going to take a look at how we can use a model that has been created in SageMaker. We will do this by first deploying our model. For us, this means using SageMaker's functionality to create an endpoint that will be used as a way to send data to our model.

> Recall, from the first lesson in this section, that an endpoint is basically a way to allow a model and an application to communicate. An application, such as a web app, will be responsible for accepting user input data, and through an endpoint we can send that data to our model, which will produce predictions that can be sent back to our application!

<img src="/Visual Representations/m6-l1-c04-endpoint.png"></p>

For our purposes an endpoint is just a URL. Instead of returning a web page, like a typical url, this endpoint URL returns the results of performing inference. In addition, we are able to send data to this URL so that our model knows what to perform inference on. We won't go too far into the details of how this is all set up since SageMaker does most of the heavy lifting for us.

An important aspect that we will encounter is that SageMaker endpoints are secured. In this case, that means that only other AWS services with permission to access SageMaker endpoints can do so.

To start with, we won't need to worry about this too much since we will be working inside of a SageMaker notebook and so we will be able to access our deployed endpoints easily.

Later on we will talk about how to set things up so that a simple web app, which doesn't need to be given special permission, can access our SageMaker endpoint.

### How to use a Deployed Model

As mentioned earlier, there are two obstacles we are going to need to overcome. The first is the security issue and the second is data processing. The way that we are going to approach solving these issues is by making use of Amazon Lambda and API Gateway.

<img src="/Visual Representations/web-app.svg"></p>

What this means is that when someone uses our web app, the following will occur.

1. To begin with, a user will type out a review and enter it into our web app.
2. Then, our web app will send that review to an endpoint that we created using API Gateway. This endpoint will be constructed so that anyone (including our web app) can use it.
3. API Gateway will forward the data on to the Lambda function
4. Once the Lambda function receives the user's review, it will process that review by tokenizing it and then creating a bag of words encoding of the result. After that, it will send the processed review off to our deployed model.
5. Once the deployed model performs inference on the processed review, the resulting sentiment will be returned back to the Lambda function.
6. Our Lambda function will then return the sentiment result back to our web app using the endpoint that was constructed using API Gateway.
7. The structure for our web app will look like the diagram below.

Don't forget!</br>
Currently our endpoint is running. The reason for this is that in the next few videos we are going to interact with our deployed endpoint. If you are following along, don't forget that your endpoint is running. If you need to take a break, don't forget to shut down your endpoint!

### Creating and Using Endpoints
You've just learned a lot about how to use SageMaker to deploy a model and perform inference on some data. Now is a good time to review some of the key steps that we've covered. You have experience processing data and creating estimators/models, so I'll focus on what you've learned about endpoints.

An endpoint, in this case, is a URL that allows an application and a model to speak to one another.

#### Endpoint steps
* You can start an endpoint by calling .deploy() on an estimator and passing in some information about the instance.

```python
xgb_predictor = xgb.deploy(initial_instance_count = 1, instance_type = 'ml.m4.xlarge')
```
* Then, you need to tell your endpoint, what type of data it expects to see as input (like .csv).
```python
from sagemaker.predictor import csv_serializer

xgb_predictor.content_type = 'text/csv'
```
xgb_predictor.serializer = csv_serializer
