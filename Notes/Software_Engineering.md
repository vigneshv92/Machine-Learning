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

Example : 

Before you begin, make sure to run this command in your terminal to install pytest:
```
pip install -U pytest
```
Then, to run pytest, just enter:
```
pytest
```
Right now, not all of the tests should pass. Fix the function to pass all its tests! Once all your tests pass, try writing some additional unit tests of your own!

##### compute_launch.py
```python
def days_until_launch(current_day, launch_day):
    """"Returns the days left before launch.
    
    current_day (int) - current day in integer
    launch_day (int) - launch day in integer
    """
    return launch_day - current_day
```

#### test_compute_launch.py
```python
from compute_launch import days_until_launch

def test_days_until_launch_4():
    assert(days_until_launch(22, 26) == 4)

def test_days_until_launch_0():
    assert(days_until_launch(253, 253) == 0)

def test_days_until_launch_0_negative():
    assert(days_until_launch(83, 64) == -19)
    
def test_days_until_launch_1():
    assert(days_until_launch(9, 10) == 1)
```

#### Test Driven Development and Data Science

* TEST DRIVEN DEVELOPMENT: writing tests before you write the code that’s being tested. Your test would fail at first, and you’ll know you’ve finished implementing a task when this test passes.

* Tests can check for all the different scenarios and edge cases you can think of, before even starting to write your function. This way, when you do start implementing your function, you can run this test to get immediate feedback on whether it works or not in all the ways you can think of, as you tweak your function.

* When refactoring or adding to your code, tests help you rest assured that the rest of your code didn't break while you were making those changes. Tests also helps ensure that your function behavior is repeatable, regardless of external parameters, such as hardware and time.

Test driven development for data science is relatively new and has a lot of experimentation and breakthroughs appearing, which you can learn more about in the resources below.

* [Data Science TDD](https://www.linkedin.com/pulse/data-science-test-driven-development-sam-savage/)
* [TDD for Data Science](http://engineering.pivotal.io/post/test-driven-development-for-data-science/)
* [TDD is Essential for Good Data Science Here's Why](https://medium.com/@karijdempsey/test-driven-development-is-essential-for-good-data-science-heres-why-db7975a03a44)
* [Testing Your Code (general python TDD](http://docs.python-guide.org/en/latest/writing/tests/)

#### Logging

Logging is valuable for understanding the events that occur while running your program. For example, if you run your model over night and see that it's producing ridiculous results the next day, log messages can really help you understand more about the context in which this occurred. Lets learn about the qualities that make a log message effective.

##### Log Messages
Logging is the process of recording messages to describe events that have occurred while running your software. Let's take a look at a few examples, and learn tips for writing good log messages.

###### Tip: Be professional and clear
```
Bad: Hmmm... this isn't working???
Bad: idk.... :(
Good: Couldn't parse file.
```

###### Tip: Be concise and use normal capitalization
```
Bad: Start Product Recommendation Process
Bad: We have completed the steps necessary and will now proceed with the recommendation process for the records in our product database.
Good: Generating product recommendations.
```

###### Tip: Choose the appropriate level for logging
```
DEBUG - level you would use for anything that happens in the program.
ERROR - level to record any error that occurs
INFO - level to record all actions that are user-driven or system specific, such as regularly scheduled operations
```

###### Tip: Provide any useful information
```
Bad: Failed to read location data
Good: Failed to read location data: store_id 8324971
```
### Code Reviews

Code reviews benefit everyone in a team to promote best programming practices and prepare code for production. Let's go over what to look for in a code review and some tips on how to conduct one.

* [Code Review](https://github.com/lyst/MakingLyst/tree/master/code-reviews)
* [Code Review Best Practices](https://www.kevinlondon.com/2015/05/05/code-review-best-practices.html)

#### Questions to Ask Yourself When Conducting a Code Review
First, let's look over some of the questions we may ask ourselves while reviewing code. These are simply from the concepts we've covered in these last two lessons!

##### Is the code clean and modular?

* Can I understand the code easily?
* Does it use meaningful names and whitespace?
* Is there duplicated code?
* Can you provide another layer of abstraction?
* Is each function and module necessary?
* Is each function or module too long?

##### Is the code efficient?
* Are there loops or other steps we can vectorize?
* Can we use better data structures to optimize any steps?
* Can we shorten the number of calculations needed for any steps?
* Can we use generators or multiprocessing to optimize any steps?

##### Is documentation effective?
* Are in-line comments concise and meaningful?
* Is there complex code that's missing documentation?
* Do function use effective docstrings?
* Is the necessary project documentation provided?

##### Is the code well tested?
* Does the code high test coverage?
* Do tests check for interesting cases?
* Are the tests readable?
* Can the tests be made more efficient?

##### Is the logging effective?
* Are log messages clear, concise, and professional?
* Do they include all relevant and useful information?
* Do they use the appropriate logging level?

### Tips for Conducting a Code Review
Now that we know what we are looking for, let's go over some tips on how to actually write your code review. When your coworker finishes up some code that they want to merge to the team's code base, they might send it to you for review. You provide feedback and suggestions, and then they may make changes and send it back to you. When you are happy with the code, you approve and it gets merged to the team's code base.

As you may have noticed, with code reviews you are now dealing with people, not just computers. So it's important to be thoughtful of their ideas and efforts. You are in a team and there will be differences in preferences. The goal of code review isn't to make all code follow your personal preferences, but a standard of quality for the whole team.
> #### Tip: Use a code linter

This isn't really a tip for code review, but can save you lots of time from code review! Using a Python code linter like pylint can automatically check for coding standards and PEP 8 guidelines for you! It's also a good idea to agree on a style guide as a team to handle disagreements on code style, whether that's an existing style guide or one you create together incrementally as a team.

> #### Tip: Explain issues and make suggestions
Rather than commanding people to change their code a specific way because it's better, it will go a long way to explain to them the consequences of the current code and suggest changes to improve it. They will be much more receptive to your feedback if they understand your thought process and are accepting recommendations, rather than following commands. They also may have done it a certain way intentionally, and framing it as a suggestion promotes a constructive discussion, rather than opposition.

```
BAD: Make model evaluation code its own module - too repetitive.

BETTER: Make the model evaluation code its own module. This will simplify models.py to be less repetitive and focus primarily on building models.

GOOD: How about we consider making the model evaluation code its own module? This would simplify models.py to only include code for building models. Organizing these evaluations methods into separate functions would also allow us to reuse them with different models without repeating code.
```

> #### Tip: Keep your comments objective
Try to avoid using the words "I" and "you" in your comments. You want to avoid comments that sound personal to bring the attention of the review to the code and not to themselves.
```
BAD: I wouldn't groupby genre twice like you did here... Just compute it once and use that for your aggregations.

BAD: You create this groupby dataframe twice here. Just compute it once, save it as groupby_genre and then use that to get your average prices and views.

GOOD: Can we group by genre at the beginning of the function and then save that as a groupby object? We could then reference that object to get the average prices and views without computing groupby twice.
```

> #### Tip: Provide code examples
When providing a code review, you can save the author time and make it easy for them to act on your feedback by writing out your code suggestions. This shows you are willing to spend some extra time to review their code and help them out. It can also just be much quicker for you to demonstrate concepts through code rather than explanations.

Let's say you were reviewing code that included the following lines:
```python
first_names = []
last_names = []

for name in enumerate(df.name):
    first, last = name.split(' ')
    first_names.append(first)
    last_names.append(last)

df['first_name'] = first_names
df['last_names'] = last_names
```

```
BAD: You can do this all in one step by using the pandas str.split method.
```

```
GOOD: We can actually simplify this step to the line below using the pandas str.split method. Found this on this stack overflow post: https://stackoverflow.com/questions/14745022/how-to-split-a-column-into-two-columns
```

```python
df['first_name'], df['last_name'] = df['name'].str.split(' ', 1).str
```
