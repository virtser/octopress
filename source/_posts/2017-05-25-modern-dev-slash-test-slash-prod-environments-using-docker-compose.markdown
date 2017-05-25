---
layout: post
title: "Modern dev/test/prod environments using Docker Compose"
date: 2017-05-25 21:24
comments: true
published: true
---
![](https://cdn-images-1.medium.com/max/800/1*s8I4jBW2KKP687LqWh3OtQ.png)

There is like thousands of post talking about what is Docker and how to start
working with it, but there is no much posts explaining simply the motivation
behind it. So I decided to write one, as I see it.

I think its much more important to understand **why** than technical details of
**how**. When you understand **why**, you have the motivation to learn **how**.

OK, let’s remind ourselves first about the old habits of how we used to work.
This to get a better reference of the problem.

We used to create dev/test/prod environments manually. It could work when your
team and environment are small. When team grows and you have to share those
dev/test environments, things start to go out of control. Such environments
aren’t isolated and become inconsistent over time.

In many cases, those environments are not identical to production environment,
running on different machines or have different network/security conditions.
Which all resulting in unexpected bugs on production.

When team and environment grows, engineers can’t keep up with constant changes
and additions of new components. It become impossible to install manually on
your local machine another dependency. This leads to creative solutions like
using some API/cache/db from another environment. 💩

This is where Docker will shine by turning your environment services
infrastructure into code. Which will be predictable, repeatable and consistent
between your engineers dev, your CI test and your production environments.

### Docker

Let’s start with **Docker**, which is the basis for everything. It takes some
time to grasp the concept and how to work with it, like with any abstraction.
But believe me it’s worth it.

Docker is using Linux core without need of creating virtual machines for each
container (service). As a result the best option as developer machine would be
Linux. Docker can run on Mac as well, but will require more resources to create
Docker virtual machine space. Sorry, I can’t provide any feedback regarding
working with Docker in Windows OS as I never tried it. (If you did, please share
your experience in comments)

What does Docker container represent? A container is a single instance of one
component in your environment. Component can be for example web application,
API, worker, cache, database, or others.

What you define in service Docker file is which OS image to use as your
baseline, how to enrich it with your service dependencies, where to copy your
code from and how to run the service.

### Docker Compose

Docker is nice when you want to spin up a single app/service. What makes it
really powerful is **Docker Compose** which creates a composition of Docker
containers that eventually represent your real application dev/test/prod
environment.

Docker composition describes the relationship between your services. Their
volumes, networks, links, configuration, etc..

It allows you to spin up the whole sandbox environment of services on your
machine. Fully isolated, your own environment. ☺

I think that’s all you need to know to get the motivation to learn how to build
Docker containers and work with Composition.

If I could explain it simply, as next step, I suggest to follow [Docker
documentation](https://docs.docker.com/learn/).

Good luck!
