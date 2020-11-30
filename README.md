# e2e Testing Workshop

In this workshop you will learn to write your first e2e tests with Selenium.
We will test a "real" website and make sure it works and keeps working as expected.


## The Testing Pyramid

"But what are e2e tests?" you might ask yourself.
Let's have a look at the testing pyramid first.

The testing pyramid is a way of thinking about the different types of automated tests and how they together create a balance and test an application from different perspectives and under different circumstances. 

![](https://user-images.githubusercontent.com/615127/100665779-91221280-3358-11eb-87e0-384b32bdea86.png)

* **Unit Tests**: Test individual components in isolation. They are usually small and fast.
* **Integration Tests**: Test different components together and verify that they work well in orchestration.
* **E2E Tests**: They test functionality as seen from the customer perspective by driving an application through its UI.

The idea of the Testing Pyramid is to find the right balance between all types of tests in our test suite, by playing to the strength of each type of test while minimizing the downsides of each one.

💡 We want to have _many more_ Unit Tests than E2E Tests.

**References** 

* [Testing Rails](https://books.thoughtbot.com/assets/testing-rails.pdf)
* [https://martinfowler.com/bliki/TestPyramid.html](https://martinfowler.com/bliki/TestPyramid.html)

## What are we going to do?


Implement e2e tests with selenium

### What is Selenium?

### The Scenario

defined test cases 
run them against "the production page"
run them against different version ("deployments") of the page

## Setup

If your are using Javascript, go to the [Javascript Selenium Template](https://github.com/wwcode-berlin-hackevenings/selenium-javascript-template) and create your own repo from it.
Follow the instructions in th template repo to setup your local enviroment to be able to run the tests.
If that does now work, the repo also has a Github Action workflow setup to run the tests as an Action.
This is less fun though because you don't get to see the browser automation in action!

As soon as you are able to run the example test, you are good to go for the next steps!

## The Test Cases

E2e tests can become very complex and implement multi-step user interactions. 
But usually you start with the basics: The first case in every test suite should be a simple test to verify that your page even exists (or that your test suite is running properly and the tests can access the page).

### Smoke Test: Verify the page loads

- got to URL
- check if anything is loading

> Run the test against v1

### Check basic elements

- check if the h1 element (the headline "Instacat") exists on the page
- check if there are (cat) images on the page
- check if the title (meta tag) is set correctly

> Run the test against v1
> Imagine a deployment happened -> run again against v2
[change className of h1 element]

### Test the like feature

...

> Run the test against v2
> Imagine a deployment happened -> run again against v3 
[break like feature to increment by > 1]

----
## Bonus Exercises

### Check if the Copyright year is correct
Is it showing the current year?

### Test the adding cats feature
Find your newly added cat on the page

### Test the "Not a Cat" Button

Allows you to flag images that are not cats to get them removed.
Remove a cat and check that it is no longer there.

### Test for no missing translations

-  Our page supports multiple languages. This means texts on our page are placeholder strings (=translation keys) in code that get replaced by the real content in different languages.
- If a key does not have a translation it looks like this: ...
- we don't want this to be shown to users, so we want a test cases, that looks for this on the whole page
[missing translation on hover tooltip text]
