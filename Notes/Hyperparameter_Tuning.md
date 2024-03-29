## Hyperparameter Tuning

In this lesson, we are going to take a look at how we can improve our models using one of SageMaker's features. In particular, we are going to explore how we can use SageMaker to perform hyperparameter tuning.

In many machine learning models there are some parameters that need to be specified by the model creator and which can't be determined directly from the data itself. Generally the approach to finding the best parameters is to train a bunch of models with different parameters and then choose the model that works best.

SageMaker provides an automated way of doing this. In fact, SageMaker also does this in an intelligent way using Bayesian optimization. What we will do is specify ranges for our hyperparameters. Then, SageMaker will explore different choices within those ranges, increasing the performance of our model over time.

In addition to learning how to use hyperparameter tuning, we will look at Amazon's CloudWatch service. For our purposes, CloudWatch provides a user interface through which we can examine various logs generated during training. This can be especially useful when diagnosing errors.

## [Introduction to Hyperparameter Tuning](https://youtu.be/nah8kxqp55U)

Let's take a look at how we can use SageMaker to improve our Boston housing model. To begin with, we will remind ourselves how we train a model using SageMaker.

Essentially, tuning a model means training a bunch of models, each with different hyperparameters, and then choosing the best performing model. Of course, we still need to describe two different aspects of hyperparameter tuning:

1) What is a bunch of models? In other words, how many different models should we train?

2) Which model is the best model? In other words, what sort of metric should we use in order to distinguish how well one model performs relative to another.

## [Boston Housing Example](https://youtu.be/lsYRtKivrGc)
