---
layout: post
title: "API Implementation"
date: 2014-01-28‎ 20:41
comments: true
published: true
---

![](/images/api.gif)

We are in the process of building of solid APIs for each of [eToro](http://www.etoro.com/) main domains. It is not an easy task at all, as we didn't invest too much in the past 7 years of eToro existence in all the architectural aspects of the system. 

How services interact with each other? Who is responsible of doing what? What are the standards that we are working with? Which tools or technology do we choose for specific task? All these questions were not answered until now. Today we start to talk and think about it along with progressing with our first real API - **User API**. It is the place where it all begins - user created for the first time, user details updated, etc...

Today we still have one Users table in our big database which holds all our customer records in addition to their basic details and more irrelevant to user stuff. Each application can update (or read) this table from code without going through a dedicated API. The problem with this approach is that there is no [single source of truth](http://en.wikipedia.org/wiki/Single_Source_of_Truth) - each and every service can apply its own business logic to change user related data, which leading to data inconsistency.

I'm taking active role of product/project manager for this API and leading the integration process with teams. Our main goals we want to achieve by User API implementation are:

1. Create the "Single Source of Truth". All the requests to register user, update it's details or get data of some user will pass through one API which hold the business logic of the user domain. We love [ServiceStack](https://servicestack.net/) and we are using their framework for our REST APIs.

2. Provide notifications of user changes to different services via Pub/Sub instead of polling database for changes like we do today. We are using [RabbitMQ](http://www.rabbitmq.com/) messaging here. 

3. Separate User related data to it's own dedicated database. This to isolate and encapsulate the user domain better. It will help in many aspects - automatic deployment of database changes with CD process, creation of environments with empty user database, other services won't effect this database performance and vice versa. We are working with [Microsoft SQL Server Data Tools](http://msdn.microsoft.com/en-us/data/tools.aspx) to accompish this

Today the User API is almost ready, but can't be completed because we need to migrate all the clients to use it instead of DB first. After all the clients which update customer records migrate, we will be able to enable caching, provide Pub/Sub functionality which can be trusted and eventually take out the user data our of the main DB to a dedicated one. 

Lessons learned so far during the API building and integration process:
 
1. Don't start it when it's too late - invest in your architecture from the beginning or at least think about it. Now it takes so many time to make the integration and fix things which were done wrongly in the past.

2. Build a good plan - development plan (phases: establishment, optimization), integration plan (insert, update, select).

3. Don't try to fix all evil at once, do it in small chunks, work iteratively. Otherwise it will hurt, it will bring more risk to migration.

4. Explain the importance of this move to the company - management and developers. It is required for engagement of people to give higher priority for integration than any other tasks.

5. Communication and follow up of progress are important to make the development and migration as fast as possible. You don't want this project to take a lifetime.