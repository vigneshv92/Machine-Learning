## Updating a Model

In this lesson we are going to take a look at updating an existing endpoint so that it conforms to a different endpoint configuration. There are many reasons for wanting to do this, the two that we will look at are, performing an A/B test and updating a model which is no longer performing as well.

To start, we will look at performing an A/B test between two different models. Then, once we've decided on a model to use, updating the existing endpoint so that it only sends data to a single model.

For the second example, it may be the case that once we've built a model and begun using it, the assumptions on which our model is built begin to change.

For instance, in the sentiment analysis examples that we've looked at our models are based on a vocabulary consisting of the 5000 most frequently appearing words in the training set. But what happens if, over time, the usage of words changes? Then our model may not be as accurate.

When this happens we may need to modify our model, often this means re-training it. When we do, we'd like to update the existing endpoint without having to shut it down. Fortunately, SageMaker allows us to do this in a straightforward way.

## [Building a Sentiment Analysis Model](https://youtu.be/dwRkA0ig3uU)

To begin with we will create an XGBoost model similar to the ones that we have constructed in the past in order to predict the median housing cost in Boston.

The difference this time is that we are using a hybrid approach, including both the high level and low level functionality. In this case we use the high level approach to train a model (to produce model artifacts) and then we use the low level approach to construct the model itself and to construct the endpoint configuration. The reason for this is so that we can have more control over how our endpoint behaves.

## [Building a Sentiment Analysis Linear Model](https://youtu.be/7TdiVF6qS1k)

Depending on the application you have in mind for a particular machine learning model, accuracy may not always be the metric you wish to optimize. There may be some other constraints on getting the model to work in production. For example, your model may not be very easy to interpret or maybe performing inference for a particular model may be too costly.

In any case you may want to try alternative models. In the example we are working on here we construct a linear learner model as an alternative to the previously created XGBoost model.

Note: It is important to notice that the result returned by the linear learner model is json, compared to the csv data returned by the XGBoost model. You can't always assume that different models will return data in the same way although typically the return type is specified in the documentation.

## [Combining Models]()
