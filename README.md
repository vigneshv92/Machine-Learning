# Syllabus

Prerequisite:
Python for Data Analysis, SQL, Command Line Essentials, Git & Github.
Additional Material: Data Visualization, Practical Statistics, Linear Algebra.

This program is all about machine learning techniques used in data science. Here is an overview of what you can expect as you move through the classroom.

## Principles of ML

* [MicrosoftLearning/Principles of Machine Learning](https://github.com/MicrosoftLearning/Principles-of-Machine-Learning-Python)

## Mathematics for ML

* [NextAI - Mathematics for ML](https://github.com/NEXTCanada/NextAI-MachineLearning)
* [Mathematics For Machine Learning](https://github.com/mml-book/mml-book.github.io)
* [ML for Beginners(Microsoft)](https://github.com/microsoft/ML-For-Beginners)

## Principles of ML

* [Research Software Engineering with Python](https://alan-turing-institute.github.io/rse-course/html/index.html)
* [UCL Research Course](http://github-pages.ucl.ac.uk/rsd-engineeringcourse/)

## Supervised, Deep, and Unsupervised Learning courses.
<img src="/Visual Representations/Types of Machine Learning.png" width="700" height="300"/></p>

## Supervised Learning
First, we'll start by teaching you how to train and test models using sklearn. We'll go over the main metrics used for evaluating models, such as accuracy, precision, recall, etc. Then, we'll learn about common supervised learning algorithms, including linear and logistic regression, decision trees, naive Bayes, neural networks, and support vector machines. We'll also learn to combine these algorithms to achieve their full potential, in the ensemble methods section. Every section is equipped with a lab, where you'll get to apply your knowledge using sklearn.

## Deep Learning
In this section, we'll be learning the foundational math and theory behind neural networks that can learn to find patterns in some given data. You'll implement backpropagation and optimization using numpy to get an understanding of neural networks, then build up to training neural networks using the deep learning framework, PyTorch. You'll see how to build your own image classifier in Pytorch.

## Unsupervised Learning
In this section, we'll be going over the main unsupervised learning algorithms, including several clustering methods, and dimensionality reduction. Unsupervised learning is all about finding groupings in data without specific metrics, like accuracy, to aim for; it is also used heavily in reducing the dimensionality of data. You'll go through several mini-projects and labs in which you'll be able to apply these concepts with real data.

This program is all about advanced machine learning techniques used in the industry. Here is an overview of what you can expect as you move through the classroom.

The content is divided into modules listed below

-----

* [handson-ml](https://github.com/ageron/handson-ml)
* [handson-ml2](https://github.com/ageron/handson-ml2)
* [Software Engineering Fundamentals](/Notes/Software_Engineering.md)
* [Machine Learning taught by Sebastian Raschka at University Wisconsin-Madison](https://github.com/rasbt/stat479-machine-learning-fs19)
* [Python Machine Learning by Sebastian Raschka](https://github.com/rasbt/python-machine-learning-book-2nd-edition)
* <b>Machine Learning in Production</b>
    * [Introduction to Deployment](/Notes/Machine_Learning_in_Production.md)
    * [Building a Model using SageMaker](/Notes/Build_Model_in_SageMaker.md)
    * [Deploying a Model](/Notes/Deploying_Model_SageMaker.md)
    * [SageMaker Deployment Notebooks](https://github.com/udacity/sagemaker-deployment)
    * [Hyperparameter Tuning](/Notes/Hyperparameter_Tuning.md)
    * [Updating a Model](/Notes/Updating_Model.md)
    
* Machine Learning Deployment Case Studies
* Build Your Own Machine Learning Portfolio (Capstone) Project.
   
* [Virgilio Data Science](https://virgili0.github.io/Virgilio/)
   >Virgilio is an open source initiative, aiming to mentor and guide anyone in the world of Data Science and Machine Learning. Our vision is to give everyone the chance to get involved in this field, get self-started as a practitioner, gain new cutting edge practical skills and learn to navigate through the infinite web of resources and find the ones useful for you.
* [Machine Learning Explainability](https://github.com/SAP/contextual-ai)
   >Contextual AI adds explainability to different stages of machine learning pipelines - data, training, and inference - thereby addressing the trust gap between such ML systems and their users. It does not refer to a specific algorithm or ML method — instead, it takes a human-centric view and approach to AI.
* [Uber’s Machine Learning Platform](https://eng.uber.com/michelangelo-machine-learning-platform/#They)
* [ML Wave](https://mlwave.com)
----

First, we'll start by teaching you some best practices for software engineering. You'll learn how to optimize your code, write tests and documentation for a code base, and build a Python package of your own. These skills are valuable in any engineering job and will act as a great foundation for applying machine learning skills in industry.

### Machine Learning in Production
In this section, you'll learn about cloud services and model deployment. Deployment means making a model available for use in a piece of hardware or web application, such as a voice assistant or recommendation engine. In this lesson, you'll see how to analyze housing data and deploy a predictive model in SageMaker. In addition to learning about model deployment, you’ll also learn about model serving and updating. You'll learn how to connect a deployed model to a website through an API using AWS services. After deploying the model, you’ll update the model to account for changes in the underlying text data—an especially valuable skill in industries that continuously collect data. By the end of this section, you should have all the skills you need to train and deploy models to solve tasks of your own design!

### Machine Learning, Deployment Case Studies
In partnership with AWS, we’ve created a course that examines a variety of machine learning models as they are applied, at-scale, to real-world tasks. You’ll learn how to deploy both unsupervised and supervised algorithms and apply them to tasks such as feature engineering and time series forecasting. This content addresses questions such as:

How do you decide on the correct machine learning model for a given task?
How can you utilize cloud deployment tools such as AWS SageMaker to work with data and improve your machine learning models?

-----

## Projects

This Nanodegree program includes four projects, which you can learn more about, below! Completing the projects will not only help you build your skills with topics like software engineering and machine learning model deployment, but also show you how those skills are used in practice and build out your technical portfolio.

Don't worry if you are not familiar with how you would even approach some of the items discussed below, you will be learning the needed skills in the lessons ahead!

### Project 1: Deploying a Sentiment Analysis Model
You have experience building and training machine learning models, and in this first project, you'll learn how to deploy a model to a production environment. Using Amazon SageMaker, you'll deploy your own PyTorch sentiment analysis model, which is trained to recognize the sentiment of movie reviews (positive or negative). Deployment gives you the ability to use a trained model to analyze new, user input. Once you deploy a trained model, you can create a gateway for accessing it from a website.
Example movie reviews.

### Project 2: Deploying a Plagiarism Detector
In this project, you'll complete a machine learning workflow, going from analyzing and exploring a corpus of text data, to extracting features that may be used to indicate plagiarism between a source and answer text. Finally, you'll upload transformed data into a SageMaker notebook instance and train and deploy a custom model for plagiarism classification! This project tests your ability to do feature engineering and model deployment.
Image depicting steps from data exploration to model deployment.

### Project 3: Capstone Project
The final project is open for you to do any project of your choosing, to add to your portfolio. One of the projects you may choose to do is a second project with the messy Arvato data. Alternatively, you might choose another project using Deep Learning to classify dog breeds. Here is a glimpse of the final project.

----

### Blogs

* [Fairness, Privacy, and Transparency by Design in AI/ML Systems](https://engineering.linkedin.com/blog/2019/fairness-privacy-transparency-by-design)
* [Responsible AI Practices](https://ai.google/responsibilities/responsible-ai-practices/)
* [Machine Learning Engineering Blogs](https://github.com/eugeneyan/applied-ml#data-engineering)
* [Microsoft Machine Learning](https://github.com/microsoft/machine-learning-collection)
* [Rules of ML](https://developers.google.com/machine-learning/guides/rules-of-ml)

### [Machine Learning System Design](https://github.com/chiphuyen/machine-learning-systems-design)
