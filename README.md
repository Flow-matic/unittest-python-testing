# unittest-python-testing

What Are Unit Tests, and Why Are They Important?
Remember doing math back in school, completing different arithmetic procedures before combining them to get the correct answer? Imagine how you would check to ensure that the calculations done at each step were correct, and you didn’t make any careless mistakes or miswrote anything.

Now, extend that idea to code! We wouldn’t want to have to constantly look through our code to statically verify its correctness, so how would you create a test to ensure that the following piece of code actually returns the area of the rectangle?

def calculate_area_rectangle(width, height):
    return width * height
We could run the code with a few test examples and see if it returns the expected output.

That’s the idea of a unit test! A unit test is a test that checks a single component of code, usually modularized as a function, and ensures that it performs as expected.

Unit tests are an important part of regression testing to ensure that the code still functions as expected after making changes to the code and helps ensure code stability. After making changes to our code, we can run the unit tests we have created previously to ensure that the existing functionality in other parts of the codebase has not been impacted by our changes.

Another key benefit of unit tests is that they help easily isolate errors. Imagine running the entire project and receiving a string of errors. How would we go about debugging our code?

That’s where unit tests come in. We can analyze the outputs of our unit tests to see if any component of our code has been throwing errors and start debugging from there. That’s not to say that unit testing can always help us find the bug, but it allows for a much more convenient starting point before we start looking at the integration of components in integration testing.

For the rest of the article, we will be showing how to do unit testing by testing the functions in this Rectangle class:

class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
 
    def get_area(self):
        return self.width * self.height
 
    def set_width(self, width):
        self.width = width
 
    def set_height(self, height):
        self.height = height
Now that we have motivated unit tests, let’s explore how exactly we can use unit tests as part of our development pipeline and how to implement them in Python!

A Gentle Introduction to Unit Testing in Python
by Zhe Ming Chng on March 3, 2022 in Python for Machine Learning
Tweet Tweet  Share
Last Updated on June 21, 2022

Unit testing is a method for testing software that looks at the smallest testable pieces of code, called units, which are tested for correct operation. By doing unit testing, we can verify that each part of the code, including helper functions that may not be exposed to the user, works correctly and as intended.

The idea is that we are independently checking each small piece of our program to ensure that it works. This contrasts with regression and integration testing, which tests that the different parts of the program work well together and as intended.

In this post, you will discover how to implement unit testing in Python using two popular unit testing frameworks: the built-in PyUnit framework and the PyTest framework.

After completing this tutorial, you will know:

Unit testing libraries in Python such as PyUnit and PyTest
Checking expected function behavior through the use of unit tests
Kick-start your project with my new book Python for Machine Learning, including step-by-step tutorials and the Python source code files for all examples.

Let’s get started!

A Gentle Introduction to Unit Testing in Python
Photo by Bee Naturalles. Some rights reserved.

Overview
The tutorial is divided into five parts; they are:

What are unit tests, and why are they important?
What is Test Driven Development (TDD)?
Using Python’s built-in PyUnit framework
Using PyTest library
Unit testing in action

What Are Unit Tests, and Why Are They Important?
Remember doing math back in school, completing different arithmetic procedures before combining them to get the correct answer? Imagine how you would check to ensure that the calculations done at each step were correct, and you didn’t make any careless mistakes or miswrote anything.

Now, extend that idea to code! We wouldn’t want to have to constantly look through our code to statically verify its correctness, so how would you create a test to ensure that the following piece of code actually returns the area of the rectangle?

def calculate_area_rectangle(width, height):
    return width * height
We could run the code with a few test examples and see if it returns the expected output.

That’s the idea of a unit test! A unit test is a test that checks a single component of code, usually modularized as a function, and ensures that it performs as expected.

Unit tests are an important part of regression testing to ensure that the code still functions as expected after making changes to the code and helps ensure code stability. After making changes to our code, we can run the unit tests we have created previously to ensure that the existing functionality in other parts of the codebase has not been impacted by our changes.

Another key benefit of unit tests is that they help easily isolate errors. Imagine running the entire project and receiving a string of errors. How would we go about debugging our code?

That’s where unit tests come in. We can analyze the outputs of our unit tests to see if any component of our code has been throwing errors and start debugging from there. That’s not to say that unit testing can always help us find the bug, but it allows for a much more convenient starting point before we start looking at the integration of components in integration testing.

For the rest of the article, we will be showing how to do unit testing by testing the functions in this Rectangle class:

class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
 
    def get_area(self):
        return self.width * self.height
 
    def set_width(self, width):
        self.width = width
 
    def set_height(self, height):
        self.height = height
Now that we have motivated unit tests, let’s explore how exactly we can use unit tests as part of our development pipeline and how to implement them in Python!


Test Driven Development
Testing is so important to good software development that there’s even a software development process based on testing, Test Driven Development (TDD). Three rules of TDD proposed by Robert C. Martin are:

You are not allowed to write any production code unless it is to make a failing unit test pass.
You are not allowed to write any more of a unit test than is sufficient to fail, and compilation failures are failures.
You are not allowed to write any more production code than is sufficient to pass the one failing unit test.
The key idea of TDD is that we base our software development around a set of unit tests that we have created, which makes unit testing the heart of the TDD software development process. This way, you are assured that you have a test for every component you develop.

TDD is also biased toward having smaller tests which means tests that are more specific and test fewer components at a time. This aids in tracking down errors, and smaller tests are also easier to read and understand since there are fewer components at play in a single run.

It doesn’t mean you must use TDD for your projects. But you may consider that as a method to develop your code and the tests at the same time.
Want to Get Started With Python for Machine Learning?
Take my free 7-day email crash course now (with sample code).

Click to sign-up and also get a free PDF Ebook version of the course.

Download Your FREE Mini-Course


Using Python Built-in PyUnit Framework
You might be wondering, why do we need unit testing frameworks since Python and other languages offer the assert keyword? Unit testing frameworks help automate the testing process and allow us to run multiple tests on the same function with different parameters, check for expected exceptions, and many others.

PyUnit is Python’s built-in unit testing framework and Python’s version of the corresponding JUnit testing framework for Java. To get started building a test file, we need to import the unittest library to use PyUnit:

import unittest
Then, we can get started writing out first unit test. Unit tests in PyUnit are structured as subclasses of the unittest.TestCase class, and we can override the runTest() method to perform our own unit tests which check conditions using different assert functions in unittest.TestCase:

class TestGetAreaRectangle(unittest.TestCase):
    def runTest(self):
        rectangle = Rectangle(2, 3)
        self.assertEqual(rectangle.get_area(), 6, "incorrect area")
That’s our first unit test! It checks if the rectangle.get_area() method returns the correct area for a rectangle with width = 2 and length = 3. We use self.assertEqual instead of simply using assert to allow the unittest library to allow the runner to accumulate all test cases and produce a report.

Using the different assert functions in unittest.TestCase also gives us a better ability to test different behaviors such as self.assertRaises(exception). This allows us to check if a certain block of code produces an expected exception.

To run the unit test, we make a call to unittest.main() in our program,

...
unittest.main()
Since the code returns the expected output for this case, it returns that the tests run successfully, with the output:

.
----------------------------------------------------------------------
Ran 1 test in 0.003s
 
OK
The complete code is as follows:

import unittest
 
# Our code to be tested
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
 
    def get_area(self):
        return self.width * self.height
 
    def set_width(self, width):
        self.width = width
 
    def set_height(self, height):
        self.height = height
 
# The test based on unittest module
class TestGetAreaRectangle(unittest.TestCase):
    def runTest(self):
        rectangle = Rectangle(2, 3)
        self.assertEqual(rectangle.get_area(), 6, "incorrect area")
 
# run the test
unittest.main()
Note: While in the above, our business logic Rectangle class and our test code TestGetAreaRectangle are put together. In reality, you may put them in separate files and import the business logic into your test code. This can help you better manage the code.

We can also nest multiple unit tests together in one subclass of unittest.TestCase, by naming methods in the new subclass with the “test” prefix, for example:

class TestGetAreaRectangle(unittest.TestCase):
    def test_normal_case(self):
        rectangle = Rectangle(2, 3)
        self.assertEqual(rectangle.get_area(), 6, "incorrect area")
 
    def test_negative_case(self): 
        """expect -1 as output to denote error when looking at negative area"""
        rectangle = Rectangle(-1, 2)
        self.assertEqual(rectangle.get_area(), -1, "incorrect negative output")
Running this will give us our first error:

F.
======================================================================
FAIL: test_negative_case (__main__.TestGetAreaRectangle)
expect -1 as output to denote error when looking at negative area
----------------------------------------------------------------------
Traceback (most recent call last):
 	File "<ipython-input-96-59b1047bb08a>", line 9, in test_negative_case
 		self.assertEqual(rectangle.get_area(), -1, "incorrect negative output")
AssertionError: -2 != -1 : incorrect negative output
----------------------------------------------------------------------
Ran 2 tests in 0.003s
 
FAILED (failures=1)
We can see the unit test that failed, which is the test_negative_case as highlighted in the output along with the stderr message since get_area() doesn’t return -1 as we expected in our test.

There are many different kinds of assert functions defined in the unittest. For example, we can use the TestCase class:

def test_geq(self):
  """tests if value is greater than or equal to a particular target"""
  self.assertGreaterEqual(self.rectangle.get_area(), -1)
We can even check whether a particular exception was thrown during execution:

def test_assert_raises(self): 
  """using assertRaises to detect if an expected error is raised when running a particular block of code"""
  with self.assertRaises(ZeroDivisionError):
    a = 1 / 0
Now, we look at building up our tests. What if we had some code that we needed to run to set up before running each test? Well, we can override the setUp method in unittest.TestCase.

class TestGetAreaRectangleWithSetUp(unittest.TestCase):
  def setUp(self):
    self.rectangle = Rectangle(0, 0)
 
  def test_normal_case(self):
    self.rectangle.set_width(2)
    self.rectangle.set_height(3)
    self.assertEqual(self.rectangle.get_area(), 6, "incorrect area")
 
  def test_negative_case(self): 
    """expect -1 as output to denote error when looking at negative area"""
    self.rectangle.set_width(-1)
    self.rectangle.set_height(2)
    self.assertEqual(self.rectangle.get_area(), -1, "incorrect negative output")
In the above code example, we have overridden the setUp() method from unittest.TestCase, with our own setUp() method that initializes a Rectangle object. This setUp() method is run prior to each unit test and is helpful in avoiding code duplication when multiple tests rely on the same piece of code to set up the test. This is similar to the @Before decorator in JUnit.

Likewise, there is a tearDown() method that we can override as well for code to be executed after each test.

To run the method only once per TestCase class, we can also use the setUpClass method as follows:

class TestGetAreaRectangleWithSetUp(unittest.TestCase):
  @classmethod
  def setUpClass(self):
    self.rectangle = Rectangle(0, 0)
The above code is only run once per TestCase instead of once per test run as is the case with setUp.

To help us organize tests and select which set of tests we want to run, we can aggregate test cases into test suites which help to group tests that should executed together into a single object:

...
# loads all unit tests from TestGetAreaRectangle into a test suite
calculate_area_suite = unittest.TestLoader() \
                       .loadTestsFromTestCase(TestGetAreaRectangleWithSetUp)
Here, we also introduce another way to run tests in PyUnit by using the unittest.TextTestRunner class, which allows us to run specific test suites.

runner = unittest.TextTestRunner()
runner.run(calculate_area_suite)
This gives the same output as running the file from the command line and calling unittest.main().

Bringing everything together, this is what the complete script for the unit test would look like:

class TestGetAreaRectangleWithSetUp(unittest.TestCase):
 
  @classmethod
  def setUpClass(self):
    #this method is only run once for the entire class rather than being run for each test which is done for setUp()
    self.rectangle = Rectangle(0, 0)
 
  def test_normal_case(self):
    self.rectangle.set_width(2)
    self.rectangle.set_height(3)
    self.assertEqual(self.rectangle.get_area(), 6, "incorrect area")
 
  def test_geq(self):
    """tests if value is greater than or equal to a particular target"""
    self.assertGreaterEqual(self.rectangle.get_area(), -1)
 
  def test_assert_raises(self): 
    """using assertRaises to detect if an expected error is raised when running a particular block of code"""
    with self.assertRaises(ZeroDivisionError):
      a = 1 / 0


The unittest unit testing framework was originally inspired by JUnit and has a similar flavor as major unit testing frameworks in other languages. It supports test automation, sharing of setup and shutdown code for tests, aggregation of tests into collections, and independence of the tests from the reporting framework.

To achieve this, unittest supports some important concepts in an object-oriented way:

test fixture
A test fixture represents the preparation needed to perform one or more tests, and any associated cleanup actions. This may involve, for example, creating temporary or proxy databases, directories, or starting a server process.

test case
A test case is the individual unit of testing. It checks for a specific response to a particular set of inputs. unittest provides a base class, TestCase, which may be used to create new test cases.

test suite
A test suite is a collection of test cases, test suites, or both. It is used to aggregate tests that should be executed together.

test runner
A test runner is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.

