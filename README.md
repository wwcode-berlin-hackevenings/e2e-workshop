# e2e Testing Workshop

In this workshop you will learn how to write your first e2e tests with Selenium.
We will test a "real" website, making sure it works and keeps working as expected.


## The Testing Pyramid

"But what are e2e tests?" you might ask yourself.
Let's have a look at the testing pyramid first.

The testing pyramid is a way of thinking about the different types of automated tests and how together they create a balance, testing an application from different perspectives and under different circumstances. 

![](https://user-images.githubusercontent.com/615127/100665779-91221280-3358-11eb-87e0-384b32bdea86.png)

* **Unit Tests**: Test individual components in isolation. They are usually small and fast.
* **Integration Tests**: Test different components together and verify that they work well in orchestration.
* **E2E Tests**: Test functionality as seen from the customer perspective by driving an application through its UI.

The idea of the Testing Pyramid is to find the right balance between all types of tests in our test suite, by playing to the strength of each type of test while minimizing the downsides of each one.

💡 We want to have _far more_ Unit Tests than E2E Tests.

**References** 

* [Testing Rails](https://books.thoughtbot.com/assets/testing-rails.pdf)
* [https://martinfowler.com/bliki/TestPyramid.html](https://martinfowler.com/bliki/TestPyramid.html)

## What are we going to do in this workshop?

In this workshop we will work in small teams to create a small e2e test suite with Selenium Webdriver.

### Team Work!

Each team works together to implement the test cases described below - you can organize yourselves however you like.
We recommend you try [Mob Programming](https://team-coder.com/mob-programming/) - Pair Programming scaled up. 
One team member will be the "driver" writing the code. All the other team members take on the "navigator" role, telling the driver what to type. 
Take turns being the "driver". If you don't feel comfortable typing, you don't have to.
There are also other ways to organize your team: Someone has to look at the documentation, someone should have the browser inspector open...

### What is Selenium?

Selenium is a tool to automate and control browsers 🤖. It's main use case is testing, but it can also be used to automate tasks.
The Selenium "family" consists of several different tools to help with the creation and execution of tests, for example an IDE.
What we will be using today is **Selenium Webdriver**, a collection of binding for different programming languages that allow us to interact with the browser.
This means we can use any of the supported programming languages and easily control the browser.

We will use this to define some user flows on our website - and then use a testing library to check if the results are as expected.

### The Workshop Scenario

During this workshop, you will take on the role of the QA (Quality Assurance) team of *Instacat* - a hot new startup in the cat social media space 🐈.
[Instacat](https://www.instacat.app) allows cats to share their cutest pictures with the world and collect likes 💜.

Your job is to work through a list of test cases that have been defined by the product team.
Each test cases describes a different user flow that uses a feature of your product.

One main reason that we write tests is to make sure new features or changes didn't break existing functionality.
This means you will run your tests against different "releases" of the instacat website - simulated by different versions.
The instructions below will tell you when a new version is released and you should change the URL you are using in your tests!

> We suggest that you start off the workshop by getting to know your new team a little!
> Tell everyone who you are, what your experience is with coding and testing and about a cat in your life!

## Setup

Select the template for your programming language of choice and create your own repo from:
- **Javascript**: [Javascript Selenium Template](https://github.com/wwcode-berlin-hackevenings/selenium-javascript-template)
- **Python**: [Python Selenium Template](https://github.com/wwcode-berlin-hackevenings/selenium-python-template)

Follow the instructions in the template repo to setup your local enviroment to be able to run the tests.
If that does not work, the (Javascript) repo also has a GitHub Action workflow setup to run the tests as an Action.
This is less fun though, because you don't get to see the browser automation in action!

As soon as you are able to run the example test, you are ready to proceed to the next steps!
The template repo also contains links to the Selenium documentation for your language of choice and for the test framework.

**Some additional links:**
- [MDN: Document Query Selector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector) - how to locate elements inside a website?
- [Selenium Main Website](https://www.selenium.dev/)
- [Guide to Browser Manipulation with Selenium](https://www.selenium.dev/documentation/en/webdriver/browser_manipulation/) - examples for different languages

> Make sure your team has at least one person who can run the example test successfully and can also share their screen. If that is all set up, you are good to proceed to the next step!
> We recommend you also make sure everyone on your team understands what is happening in the example test before you start writing your own!

## The Test Cases

We have described a few test cases below, starting from very basic with no interactions and increasing in complexity.
Feel free to go through them one by one or skip ahead!


### Smoke Test: Verify the page loads

E2e tests can become very complex and implement multi-step user interactions. 
But usually you start with the basics: 
The first case in every test suite should be a very simple test to verify that your page even loads at all (or that your test suite is running properly and the tests can access the page).

1. Use selenium to navigate to the Instacat website https://www.instacat.app
2. Verify that anything is loading: You can for example select an appropriate element with selenium and check if it exists on the website using the testing library

> Run your new test case and see if it is successful (green)

Congratulations! You have written your first test! 🙌

 💡 **Tips**
- Look for the "get" method of the webdriver class to navigate to a URL
- Your test can check for the existence of a certain element on the page, but there are also other options available. 
- The browser dev tools with the inspector are your best friends 👫

### Check basic elements

In this test case we want to look for specific HTML elements that should always be present on our website.

1. Use selenium to navigate to the Instacat website
2. Check if the h1 element (the headline "Instacat") exists on the page (use selenium to select it and the testing library to assert that it exists)
3. Bonus: Check if there are any images on the page (we expect at least one image)
4. Bonus: Check if the title meta tag is set correctly (we expect it to be "Instacat")

> Run your test against the first version of the website from the previous test case

If everything is green, congratulations again - you already finished 2 test cases!

> Now imagine a new version of the Instacat website was deployed and some changes have been made to the website
> Update the URL in your test to https://v2.instacat.app/ and run the tests again. Are all test cases still green?

<details> 
  <summary><i>Why is my test failing now?</i></summary>
   Tests fail for different reasons - sometimes because they are not robust against changes in the code. We want our tests to only fail when the functionality has changed / is broken. We try to write them in a way that they are robust against non-functional changes.
  
  
  In this case, the only thing that changed are some CSS classes. If you used those to find the elements, your test might fail, even though the functionality of the site is unchanged.
Depending on the project it can be a bad choice to use CSS classnames as selectors, if those classes might change frequently. 
  A good way to select an element is a special data-test-id attribute (when it is available).
</details>


 💡 **Tips**
- You might want to extract the URL to a variable so you don't have to change it for all your test cases after each deployment.
- You can use the find element function to look for specific HTML elements on a page
- There is a special function to check the value of the page title

### Test the like feature

All that the cats of Instacat want are likes! The like feature is really important, so we want to be sure it works.
Write a test case where the like button is clicked and we check that the like counter has in fact increased.

1. Navigate to the Instacat website using selenium
2. Find the like counter (of any cat) with selenium and store its value
3. Find the like button (of the same cat!)
4. Click the like button using selenium
5. Check the value of the like counter again - is it higher than before?

> Run the test against the previous version of instacat https://v2.instacat.app/

If everything is green, we can be confident that our test suite will alert us when a change break this core feature of Instacat!

> Imagine that another deployment happened, so you need to run your tests against the new version https://v3.instacat.app/ to verify that everything still works

<details> 
  <summary>Why is my test failing? </summary>
Sometimes tests fail because there is a bug 🐞 in our software - this is where they shine and where we want them to fail! It gives us a chance to fix the bug before it goes to production and affects our fluffy users.
  
  In this version, a bug was introduced to the like feature - you should be able to see it easily when you do a manual test.
  
  So in this case the failing test was a good thing! It alerted us to a bug in the software that we can fix now.
</details>


 💡 **Tips**
- If you have found an element, you get back a Web Element: This object exposes different methods to allow you to interact with it.

----
## Bonus Exercises

Congratulations, you were really fast! Here are a few bonus cases if you want to write some more tests.

### Check if the Copyright year is correct (easy)

The page footer shows a Copyright notice.
Make sure it is showing the current year and is not outdated!

> Run your test against the previous version 3 and see what happens (you can probably tell what happens from looking at the website...)

<details> 
  <summary>Why is my test failing? </summary>
You found another bug: The date was from last year. Again your test suite saves the day!
</details>

> Your tests found two bugs already. Luckily the developers have deployed a new version that fixes both those issues: https://v4.instacat.app/  

Your tests should be green again.

### Test the adding cats feature (complex)

One of the main features of instacat is adding new cats and their cute pictures.
Write a test case for the whole flow of adding a new cat with an image and verify this cat is shown on the website.
For this test you need to interact with the form fields, enter values and submit them.
Wait until the new entry has been added to the page and check if your new cat is showing up.

 💡 **Tips**
 - Usually an interaction like adding a new element takes a while because the request has to be sent to a server and the page has to wait for a response. So you might have to make sure your test waits a little until the server response has arrived before checking for the new cat entry.

### Test the "Not a Cat" Button

Users can flag inappropriate content - anything that is not a cat. Instacat is just for cats after all!
If the "Not a Cat" button is clicked, the questionable entry should be removed from the site.
Write a test case for the whole flow of clicking the button and checking that entry is gone afterwards.

