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

<img src="/Visual Representations/model-app-endpoint.png"></p>

#### Endpoint steps
* You can start an endpoint by calling .deploy() on an estimator and passing in some information about the instance.

```python
xgb_predictor = xgb.deploy(initial_instance_count = 1, instance_type = 'ml.m4.xlarge')
```
* Then, you need to tell your endpoint, what type of data it expects to see as input (like .csv).
```python
from sagemaker.predictor import csv_serializer

xgb_predictor.content_type = 'text/csv'
xgb_predictor.serializer = csv_serializer
```
* Then, perform inference; you can pass some data as the "Body" of a message, to an endpoint and get a response back!
```python
response = runtime.invoke_endpoint(EndpointName = xgb_predictor.endpoint,   # The name of the endpoint we created
                                       ContentType = 'text/csv',                     # The data format that is expected
                                       Body = ','.join([str(val) for val in test_bow]).encode('utf-8'))
 ```
* The inference data is stored in the "Body" of the response, and can be retrieved:

```python
response = response['Body'].read().decode('utf-8')
print(response)
```
* Finally, do not forget to shut down your endpoint when you are done using it.
```
xgb_predictor.delete_endpoint()
```

### Building a Lamda Function
[Lamda Function](https://youtu.be/jOXETK4AerU)

In general, a Lambda function is an example of a 'Function as a Service'. It lets you perform actions in response to certain events, called triggers. Essentially, you get to describe some events that you care about, and when those events occur, your code is executed.

For example, you could set up a trigger so that whenever data is uploaded to a particular S3 bucket, a Lambda function is executed to process that data and insert it into a database somewhere.

One of the big advantages to Lambda functions is that since the amount of code that can be contained in a Lambda function is relatively small, you are only charged for the number of executions.

In our case, the Lambda function we are creating is meant to process user input and interact with our deployed model. Also, the trigger that we will be using is the endpoint that we will create using API Gateway.

#### Create a Lambda Function
The steps to create a lambda function are outlined in the notebook and here, for convenience.

Setting up a Lambda function The first thing we are going to do is set up a Lambda function. This Lambda function will be executed whenever our public API has data sent to it. When it is executed it will receive the data, perform any sort of processing that is required, send the data (the review) to the SageMaker endpoint we've created and then return the result.

#### Part A: Create an IAM Role for the Lambda function

Since we want the Lambda function to call a SageMaker endpoint, we need to make sure that it has permission to do so. To do this, we will construct a role that we can later give the Lambda function.

#### Part B: Create a Lambda function

Now it is time to actually create the Lambda function. Remember from earlier that in order to process the user provided input and send it to our endpoint we need to gather two pieces of information:

* The name of the endpoint, and
* the vocabulary object.
* We will copy these pieces of information to our Lambda function, after we create it.

```python
 We need to use the low-level library to interact with SageMaker since the SageMaker API
# is not available natively through Lambda.
import boto3

# And we need the regular expression library to do some of the data processing
import re

REPLACE_NO_SPACE = re.compile("(\.)|(\;)|(\:)|(\!)|(\')|(\?)|(\,)|(\")|(\()|(\))|(\[)|(\])")
REPLACE_WITH_SPACE = re.compile("(<br\s*/><br\s*/>)|(\-)|(\/)")

def review_to_words(review):
    words = REPLACE_NO_SPACE.sub("", review.lower())
    words = REPLACE_WITH_SPACE.sub(" ", words)
    return words

def bow_encoding(words, vocabulary):
    bow = [0] * len(vocabulary) # Start by setting the count for each word in the vocabulary to zero.
    for word in words.split():  # For each word in the string
        if word in vocabulary:  # If the word is one that occurs in the vocabulary, increase its count.
            bow[vocabulary[word]] += 1
    return bow


def lambda_handler(event, context):

    vocab = "*** ACTUAL VOCABULARY GOES HERE ***"

    words = review_to_words(event['body'])
    bow = bow_encoding(words, vocab)

    # The SageMaker runtime is what allows us to invoke the endpoint that we've created.
    runtime = boto3.Session().client('sagemaker-runtime')

    # Now we use the SageMaker runtime to invoke our endpoint, sending the review we were given
    response = runtime.invoke_endpoint(EndpointName = '***ENDPOINT NAME HERE***',# The name of the endpoint we created
                                       ContentType = 'text/csv',                 # The data format that is expected
                                       Body = ','.join([str(val) for val in bow]).encode('utf-8')) # The actual review

    # The response is an HTTP response whose body contains the result of our inference
    result = response['Body'].read().decode('utf-8')

    # Round the result so that our web app only gets '1' or '0' as a response.
    result = round(float(result))

    return {
        'statusCode' : 200,
        'headers' : { 'Content-Type' : 'text/plain', 'Access-Control-Allow-Origin' : '*' },
        'body' : str(result)
    }
```

### Building an API

[API](https://youtu.be/AzBQ-aDQSG4)

At this point we've created and deployed a model, and we've constructed a Lambda function that can take care of processing user data, sending it off to our deployed model and returning the result. What we need to do now is set up some way to send our user data to the Lambda function.

The way that we will do this is using a service called API Gateway. Essentially, API Gateway allows us to create an HTTP endpoint (a web address). In addition, we can set up what we want to happen when someone tries to send data to our constructed endpoint.

In our application, we want to set it up so that when data is sent to our endpoint, we trigger the Lambda function that we created earlier, making sure to send the data to our Lambda function for processing. Then, once the Lambda function has retrieved the inference results from our model, we return the results back to the original caller.

### Using the Final Web Application

[Web App](https://youtu.be/VgG41Q_a15I)

Now we get to reap the rewards of all our hard work, we get to deploy our web app!

The back end of our app has been set up so at this point all we need to do is finish up the user facing portion, the website itself. To do this we just need to tell our website where it should send data to.

### Don't forget!
In order for our web app to work, we need to have our model deployed. This means that we are incurring a cost. So, once you have finished playing with your newly created web app, make sure to shut it down!

You may also want to clean up the endpoint that you constructed and the Lambda function. This isn't too important, however, since each of these services only incur a cost when used.

#### Some notes on Lambda and Gateway usage

For Lambda functions you are only charged per execution, which for this class will be very few and still within the free tier. Deleting a lambda function is just a good cleanup step; you won't be charged if you just leave it there (without executing it). Similarly, for APIs created using API Gateway you are only charged per request, and the number of requests we require in this course should still fall under the free tier.

### What have we learned so far?
In this lesson we learned how to deploy a model that has been created using SageMaker. We took a look at how to construct endpoints and how to use those endpoints to send data to a deployed model.

In addition, we looked at what we needed to do if we wanted anyone to have access to our deployed model. To make this work we first implemented a Lambda function that took care of data processing and interacting with the model. Then we created an interface through which we could send data to our Lambda function using API Gateway.

### What's next?
In the next lesson we are going to look at hyperparameter tuning. This is a method by which we can test a variety of different hyperparameters and chose the ones that work best for our data set.

While doing this we will also take a look at CloudWatch, which is a service that allows us to look at the logs generated by the various SageMaker tasks we perform.
