---
layout: post
title: "How I recruited test automation engineer"
date: 2015-05-13 11:20
comments: true
published: true
---

![](/images/test_automation.jpg)

Before we begin, I just want to make sure that we are on the same page about what is  "Test Automation". For me, it is a way to automatically validate that a real user experiencing the predicted application behaviour. For example: User click on a button which should open a new window. In this case we need to automatically validate that user is able to click a button and a window will show up with predefined text. [Wikipedia: Test automation](http://en.wikipedia.org/wiki/Test_automation)

Ideally, I wouldn't recruit a test automation engineer at all. I beleive that software engineers should be capable to test their own code (as part of "[eat your own dog food](http://en.wikipedia.org/wiki/Eating_your_own_dog_food)" concept) by writing unit, integration or end to end tests. It makes even a higher level of bond to the code that you are developing and need to maintain in the future.

But in reality, there are many reasons that might prevent you from living without QA position at all. It could be a culture of the organization that you are working in, legacy code that you need to deal with, could be the product nature that you are developing and etc... Moreover, you might need someone to own quality control in your organization.

My team was missing a QA person to take control of the product quality that we were  developing and take ownership of quality all in all. We wanted to do 80% of the testing automatically while covering the manual in the left 20%. I had a budget to recruit test automation engineer of junior to mid level.

How do you recruit a good junior engineer? You are looking for a potential which you need to find and validate by testing it. So I composed a simple exercise for test automation position interview. I gave it as homework after meeting a potential candidate which passed the initial screening.

I thought that it would be a nice exercise to use some SaaS tools to check our company website contact form. I choose to use [Saucelabs](https://saucelabs.com) for test automation code execution in the cloud using Selenium web driver and [Loader](https://loader.io) to do the load test.

I tried to make the test work myself, before I give this exercise for candidate, to make sure that it's possible and to learn the field myself to feel more eligible. (I never did test automation before)

The main purpose of the exercise was to see how candidate can learn and deal with new tools, use them to write automation and summarize all his work in a document describing what and why it was done.

I sent the exercise as homework to few candidates asking them to send me results in 24 hours, including the test automation source code and document explaining the services and the work that was done.

Eventually I found this approach of testing candidates very effective. You could see weak candidates return partial test results or not returning results of tests at all. Strong candidates asked question and tried to accomplish the mission in the best way. Some even found bugs in our contact form by running their unique tests. :)

Hope you find it interesting. If you have any question, let me know.