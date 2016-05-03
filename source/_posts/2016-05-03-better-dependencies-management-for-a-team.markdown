---
layout: post
title: "Better dependencies management for a team"
date: 2016-05-03 20:07
comments: true
published: true
---

![](https://cdn-images-1.medium.com/max/800/1*R9aL9QgxtcS_lXOcXODvSw.jpeg)

When you are like me working in a team of web engineers, on a project which involves usage of external 3rd party libraries and you are using [_npm_](https://www.npmjs.com/) and/or [_bower_](http://bower.io/) to manage those dependencies, you probably will find it useful.

## The problem:

When you are working in a team and you are not keeping the 3rd party dependencies as part of your repository. Someone decides to add/remove/upgrade some dependency, they modify _package.json_ or _bower.json_ files reflecting the change and submits the change into repository.

Now you pull those changes into your local copy of the project and unless you run manually _npm install_ and _bower install_ you won’t have those dependencies updated for you locally. Which in most cases result to build/run errors or inconsistency.

## The solution:

As we are working with [grunt](http://gruntjs.com/), I wrote a small [grunt task](https://www.npmjs.com/package/grunt-local-deps-update) which helps detect and update dependencies if _package.json_ or _bower.json_ files version was changed.

So from now on, when someone changes a dependency and bumps npm/bower version, grunt task will automatically update every team member local dependencies.

Which eliminates notifications, questions and increases productivity. :)

Feel free to use it:   
[https://www.npmjs.com/package/grunt-local-deps-update](https://www.npmjs.com/package/grunt-local-deps-update)