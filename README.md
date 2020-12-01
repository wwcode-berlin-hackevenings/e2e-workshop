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

## What are we going to do in this workshop?

In this workshop we will work in small teams to create a small e2e test suite with Selenium Webdriver.
Each team works together to implement the test cases described below - you can organize yourselfs however you like.
We recommend you try [Mob Programming](https://team-coder.com/mob-programming/) - Pair Programming scaled up. This means you will take turn being the "driver" writing the code. 
All other team members take on the "navigator" role, telling the driver what to type.
If you don't feel comfortable typing, you don't have to.
There are also other ways to organize your team: Someone has to look at the documentation, someone should have the browser inspector open...

### What is Selenium?

Selenium is a tool to automate and control browsers 🤖. It's main use case is testing, but it can also be used to automate tasks.
The Selenium "family" consists of multiple different tools to help with the creation and execution of tests, for example an IDE.
What we will be using today is **Selenium Webdriver**, a collection of binding for different programming languages that allow us to interact with the browser.
This means we can use any of the supported programming languages and easily control the browser.

We will use this to define some user flows on our website - and then use a testing library to check if the results are as expected.

### The Scenario

During this workshop, you will take on the role of the QA (Quality Assurance) team of *Instacat* - a hot new startup in the cat social media space 🐈.
[Instacat](https://www.instacat.app) allows cats to share their cutest pictures with the world and collect likes 💜.

Your job is to work through a list of test cases that have been defined by the product team
Each test cases describes a different user flow that uses a feature of your product.

One main reason why we write tests is to make sure new features or changes didn't break existing functionality.
This means you will run your tests against different "releases" of the instacat website - simulated by different versions.
The instructions below will tell you when a new version is released and you should change the URL you are using in your tests!

## Setup

If your are using **Javascript**, go to the [Javascript Selenium Template](https://github.com/wwcode-berlin-hackevenings/selenium-javascript-template) and create your own repo from it.
Follow the instructions in the template repo to setup your local enviroment to be able to run the tests.
If that does now work, the repo also has a Github Action workflow setup to run the tests as an Action.
This is less fun though because you don't get to see the browser automation in action!

As soon as you are able to run the example test, you are good to go for the next steps!
The template repo also contains links to the documentation of Selenium for your language of choice and for the test framework.

**Some additional links:**
- [MDN: Document Query Selector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector) - how to locate elements inside a website?
- [Selenium Main Website](https://www.selenium.dev/)
- [Guide to Browser Manipulation with Selenium](https://www.selenium.dev/documentation/en/webdriver/browser_manipulation/) - examples for different languages

## The Test Cases

E2e tests can become very complex and implement multi-step user interactions. 
But usually you start with the basics: 
The first case in every test suite should be a very simple test to verify that your page even loads at all (or that your test suite is running properly and the tests can access the page).

### Smoke Test: Verify the page loads

1. Navigate to the Instacat website https://www.instacat.app
2. Verify that anything is loading: Pick an appropriate element and check if it exists on the website

> Run your tests!

**Tipps**
- Look for the "get" method of the webdriver class to navigate to a URL
- Your test can check different things, one option could be to find a certain element

### Check basic elements

This time we want to look for very specific elements that should always be present on our website.

1. Navigate to the Instacat website
2. Check if the h1 element (the headline "Instacat") exists on the page
3. Bonus: check if there are any images on the page (we expect at least one image)
4. Bonus: check if the title meta tag is set correctly

> Run your test against the first version of the website from the previous test case

Now imagine a new version was deployed and some changes have been made to the website:

> Update the URL in your test to https://v2.instacat.app/ and run the tests again. Are all test cases still green?

*Tests fail for different reasons - sometimes because they are not robust against changes in the code*

**Tipps**
- You might want to extract the URL to a variable so you don't have to change it for all your test cases after each deployment.
- You can use the find element function to look for specific HTML elements on a page
- There is a special function to check the value of the page title

### Test the like feature

All that the cats of Instacat want are likes! The like feature is really important, so we want to be sure it works.
Write a test case where the like button is clicked and we check that the like counter has in fact increased.

1. Navigate to the Instacat website
2. Find the like counter (of any cat) and store its value
3. Find the like button (of the same cat!)
4. Click the like button
5. Check the value of the like counter again - is it higher than before?

> Run the test against the previous version of instacat

> Again a deployment happened, so you need to run again against the new version https://v3.instacat.app/ to verify that everything still works

*Sometimes tests fail because there is a bug 🐞 in our software - this is where they shine and where we want them to fail! It gives us a chance to fix the bug before it goes to production and affects our fluffy users.*

**Tipps**
- If you have found an element, you get back a Web Element: This object exposes different methods to allow you to interact with it.

----
## Bonus Exercises

Congratulations, you were really fast! Here are a few bonus cases if you want to write some more tests

### Check if the Copyright year is correct (easy)

The page footer shows a Copyright notice.
Make sure it is showing the current year and is not outdated!

> You found another bug! Here is the new version that fixes it: https://v4.instacat.app/  Your tests should be green again!

### Test the adding cats feature (complex)

One of the main features of instacat is adding new cats and their cute pictures.
Write a test case for the whole flow of adding a new cat with an image and verify this cat is shown on the website.

### Test the "Not a Cat" Button

Users can flag inappropriate content - anything that is not a cat. Instacat is just for cats after all!
If the "Not a Cat" button is clicked, the questionable entry should be removed from the site.
Write a test case for the whole flow of clicking the button and checking that entry is gone afterwards.

