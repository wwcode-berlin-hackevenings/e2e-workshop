# e2e Testing Workshop

In this workshop you will learn to write your first e2e tests with Selenium.
We will test a "real" website and make sure it works and keeps working as expected.


## The Testing Pyramid

"But what are e2e tests?" you might ask yourself.
Let's have a look at the testing pyramid first.
...

## What are we going to do?


Implement e2e tests with selenium

### What is Selenium?

### The Scenario

defined test cases 
run them against "the production page"
run them against different version ("deployments") of the page

## Setup

- link to different sections / files for setup with JS, Python...

## The Test Cases

E2e tests can become very complex and implement multi-step user interactions. 
But usually you start with the basics: The first case in every test suite should be a simple test to verify that your page even exists (or that your test suite is running properly and the tests can access the page).

### Smoke Test: Verify the page loads

- got to URL
- check if anything is loading

> Run the test against v1

### Check basic elements

- check if the title element (the headline "Instacat") exists on the page
- check if there are (cat) images on the page

> Run the test against v1
> Imagine a deployment happened -> run again against v2

### Test the like feature

...

> Run the test against v2
> Imagine a deployment happened -> run again against v3
> Imagine you run the test regularly -> run again against v4


----
## Bonus Exercises

### Test the adding cats feature

...

### Test the "Not a Cat" Button

Allows you to flag images that are not cats to get them removed.

### Test for no missing translations

-  Our page supports multiple languages. This means texts on our page are placeholder strings (=translation keys) in code that get replaced by the real content in different languages.
- If a key does not have a translation it looks like this: ...
- we don't want this to be shown to users, so we want a test cases, that looks for this on the whole page
