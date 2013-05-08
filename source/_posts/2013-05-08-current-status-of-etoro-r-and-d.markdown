---
layout: post
title: "Current status of eToro R&amp;D"
date: 2013-05-08 22:35
comments: true
published: true
---

![](/images/eToro.jpg)

When I refer to current R&D status, I refer to the situation which was relevant for about 3 months ago. Not that today it is very  different, but what started in [eToro] 3 months ago I'm going to call the future of [eToro] R&D. And I'm going to cover it in next  post.

Anyway, lets talk about the current R&D status. We are big and we are getting bigger all the time. We are about 70 employees in R&D (including developers, QA, DBAs and IT).

We have migrated from SVN to Mercurial revision control system. SVN was really bad with dealing with branch merges. Openbook was a big team of 8 people and it was impossible to continue with SVN. We wanted to work using [feature branch model](http://nvie.com/posts/a-successful-git-branching-model/). Our only two candidates were Git and Mercurial, both are very similar and fit our needs. We chose Mercurial because we are using [FogBugz](http://www.fogcreek.com/fogbugz/) as our bug tracking system and FogCreek released [Kiln](http://www.fogcreek.com/kiln/), a Mercurial server which has a tight integration with FogBugz.

Shared static environments problems is a daily talk and everybody knows that dealing with configuration changes or fixing a broken environment can take hours, sometimes days. There is no integration environment where we can test cross R&D developments. We have to work in the office, because we are dependant in our network, we have no mocks.

We have a lot of dependencies, we wait for QA to finish, we wait for DBA to write the script, we wait for IT to deploy application, we wait for IT to see our logs in production in case of troubleshooting. We are doing blocking development.

We have sort of monitoring in production using [LogEntries](https://logentries.com/) and [New Relic](http://newrelic.com/) which gives us more information, but we still can't find the source of the problem when we have crisis.

In the past year we slowly started to learn and implement Test Driven Development process in few teams, writing unit tests. Still not enough, product can hardly understand/feel the impact of these tests. Same goes with peer code reviews. We have no test automation at all, our manual regression test takes 3 days of 2 QA people.

About a year ago we recruited configuration manager who started with build automation in teams. Nowadays most of the projects are built automatically. Deployments are still done manually to all environments. 

We have no performance test lab, but we already starting to feel the impact of customers growth in production. All the problems are found in productions.

We have very few DBs, some are really big with a lot of shared objects, no APIs on shared objects. We have no scripts to create clean DB with just the schema. Our DBs should be separated to small DBs. DB revision control is awkward.

In the last year we made a transition in most of the teams from Waterfall to Agile software development methodology. It gave us a new breath, short releases (once in 2-3 weeks), more visibility of the process, tools to measure the process and get improved. From other hand it also emphasized our downsides, our dependencies, risks we take. It is still hard to manage it, we have delays in iterations, we commit to stories which we don't deliver and we deliver stories which we didn't commit to.

We feel that we are not scalable internally. We afraid to recruit another team member, because it won't increase our performance, it will decrease it and I was able to prove that.

It is a heavy and slow machine which can hardly move...

P.S.
Next post will be much more positive. ;)


[eToro]: http://www.etoro.com