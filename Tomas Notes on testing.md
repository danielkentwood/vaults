# Tomas Notes on testing

Created: August 25, 2020 5:15 PM
Updated: August 25, 2020 5:15 PM

Testing in Python

- unit tests: test that is supposed to test an isolated unit of functionality (one method, object, etc.)
- regression tests: someone complains about a bug, create a ticket in a bug tracker, you want to make sure the bug doesn't happen again. So the bug is fixed, but you have a special test that specifically tests for that bug to make sure it never happens again.
- integration test: whether multiple components that comprise a system can work well together. e.g., software architecture like microservices (instead of monolith) are split into smaller cooperating services. Imagine creating a product that is monitoring fridge contents and tells you what to buy. You might have sensor in fridge, sends data to cloud endpoint (first microservice), processing of picture to identify objects in picture (second), send to another service that compares contents identified with your desired contents (third microservice), etc. You need tests that make sure the individual systems haven't changed, and if they have, that they don't break the interoperation.

Continuous integration is controlled by a yaml file saved in the repository.

Exit codes:

- any number between 0 and 255
- no convention except 0 is success and everything else is not success
- echo $? $? is the name of the environment variable that stores the exit code of the previous command. This will let you know if the previous command was successful or not.

try using Docker

**pytest**

running pytest in the directory will look for files in the directory that have the tests

1. import the method you want to test
2. create a function that tests the method you want to test
3. think about all of the inputs you would pass to method
4. call the method you want to test while using a test case that you think might come up
5. use assert to verify expectations
6. Do this for every edge case you can imagine
7. Try to break your code (think about wrong data types, wrong data size, etc.). Think about all of the assumptions your code makes about the inputs.
8. save the test.py file
9. run it with: pytest package/test.py

for a collection of python of python packages, you need

1. __init__.py
2. for subpackage (e.g., submodules for a method), you need __init__.py on that level too.

**Mocking or monkey-patching**

- want to make sure that your tests are failing for the reasons you think they are
- Don't want your unit tests to become integration tests unintentionally.
- Create a small version of the thing you are trying to test instead of testing the whole thing.

**Engineering tips**

- classes are always with CamelCase
- snake_case for variables, methods
- use 4 spaces instead of a tab
- Don't leave commented code in your Main
- Always use docstrings!
- use parentheses
- when you're calling a function, you don't use spaces around equals for input into the function, but have spaces after the commas separating arguments
- imports should be sorted in the following way
    - at the top are standard python
    - then 3rd party
    - then your own packages
    - separated by spaces
- Write a docstring for the module file itself

vim ~/.vimrc