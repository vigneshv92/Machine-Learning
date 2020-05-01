----
## Welcome To Software Engineering Practices Part I
----
In this lesson, you'll learn about the following practices of software engineering and how they apply in data science.

* Writing clean and modular code
* Writing efficient code
* Code refactoring
* Adding meaningful documentation
* Using version control

In the lesson following this one (Part II) you'll also learn these software engineering practices:

* Testing
* Logging
* Code reviews

----

### Code Refactoring 

### Code Optimisation

### Model Versioning

In the previous example, you may have noticed that each commit was documented with a score for that model. This is one simple way to help you keep track of model versions. Version control in data science can be tricky, because there are many pieces involved that can be hard to track, such as large amounts of data, model versions, seeds, hyperparameters, etc.

Here are some resources for useful ways and tools for managing versions of models and large data. These are here for you to explore, but are not necessary to know now as you start your journey as a data scientist.
On the job, you’ll always be learning new skills, and many of them will be specific to the processes set in your company.

[How to Version Control Your Production Machine Learning Models](https://blog.algorithmia.com/how-to-version-control-your-production-machine-learning-models/)

### Testing 
#### Unit Tests
We want to test our functions in a way that is repeatable and automated. Ideally, we'd run a test program that runs all our unit tests and cleanly lets us know which ones failed and which ones succeeded. Fortunately, there are great tools available in Python that we can use to create effective unit tests!

#### Unit Test Advantages and Disadvantages
The advantage of unit tests is that they are isolated from the rest of your program, and thus, no dependencies are involved. They don't require access to databases, APIs, or other external sources of information. However, passing unit tests isn’t always enough to prove that our program is working successfully. To show that all the parts of our program work with each other properly, communicating and transferring data between them correctly, we use integration tests. In this lesson, we'll focus on unit tests; however, when you start building larger programs, you will want to use integration tests as well.

You can read about integration testing and how integration tests relate to unit tests [here.](https://www.fullstackpython.com/integration-testing.html) That article contains other very useful links as well.

#### Unit Testing Tools
To install pytest, run pip install -U pytest in your terminal. You can see more information on getting started [here.](https://docs.pytest.org/en/latest/getting-started.html)

Create a test file starting with test_
Define unit test functions that start with test_ inside the test file
Enter pytest into your terminal in the directory of your test file and it will detect these tests for you!
test_ is the default - if you wish to change this, you can learn how to in this pytest [configuration](https://docs.pytest.org/en/latest/customize.html)

In the test output, periods represent successful unit tests and F's represent failed unit tests. Since all you see is what test functions failed, it's wise to have only one assert statement per test. Otherwise, you wouldn't know exactly how many tests failed, and which tests failed.

Your tests won't be stopped by failed assert statements, but it will stop if you have syntax errors.
