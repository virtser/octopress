---
layout: post
title: "History of development process in eToro"
date: 2013-05-01 08:02
comments: true
published: true
---
![First eToro logo - 2007](/images/logo.jpg)

It's all started for me about 6 years ago, summer 2007. I left another startup in gambling industry in favor of [eToro], which looked very promising to me. I had an experience of few years as webmaster and web developer and I was at my last year of computer science studies in a collage. My main mission was to establish company websites.

We were very few developers in a fresh new startup company. And as any typical Israeli startup company of these years our focus was to build and deliver our products as fast as possible.

There were about 5 developers all in all when each was responsible to cover products in multiple fields. As web developer I was responsible
to build and maintain company websites, Affiliates system and Billing front-end.

In the first year the development process was almost unmanaged. We got requirements and requests for development by email or during a short brainstorm meeting in our CEO ([Yoni Assia](http://yoniassia.com)) office. We had no revision control system, neither bug tracking system. And it all worked fine, as soon as we were a small team.

About a year later, as our needs and requirements increased, we had to recruit more developers to the teams. R&D teams started to grow. We got more and more emails with development requests which we passed from one to other. It was endless email threads which can be hardly tracked.

At this point we decided to install our first revision control system to make audit of changes - [Microsoft Source Safe](http://en.wikipedia.org/wiki/Microsoft_Visual_SourceSafe). It was a real pain in the a*s to use it. It was eventually replaced by SVN which is better, but in bigger teams we had a branch merge hell with it.

Later on we also installed simple and intuitive bug tracking system which we are still using - [FogBugz](http://www.fogcreek.com/fogbugz/). We have .NET stack here for 80% of our products, that was the main reason for using these tools.

We had dedicated QA team which did only "monkey testing". We had no automation at all. No unit tests, integration test, test automation, performance test, load test. Nobody invested time in peer code reviews. Logs were a mess, same with monitoring. It was very hard to find and identify the source of the problem.

Our development was done on personal computers and we used them as our environments as well. Shared resources. Each team member could break others environment with his change.

No REST APIs at all, instead DLLs everywhere we need to communicate with other internal components.

Product lead R&D but not the opposite. Developers has almost no power to decide.

We worked in waterfall software development methodology although it wasn't formal. Our releases was very long and risky. It took months to release following by weeks to fix bugs of such big release.

And so on and on, you get the picture, right?

It was a nightmare...

In the next post I’m going to describe the current R&D situation in [eToro].

[eToro]: http://www.etoro.com