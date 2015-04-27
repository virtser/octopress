---
layout: post
title: "Jasmine testing tips"
date: 2015-04-19 19:15
comments: true
published: true
---

If you are developing web application and you are working on client side, I hope you write unit tests or test automation or even both like we do. The following tips might be helpful if you write your tests using [Jasmine](http://jasmine.github.io/) and execute it with [Karma](http://karma-runner.github.io/) or [Protractor](http://angular.github.io/protractor/).

I guess you already know that if you want to disable a specific test you can add "x" before _describe_ or _it_ statements? 

```
xdescribe('my beautiful function', function() {
 xit('having fun', function() {

 });
});
```

Did you also know that if you add "d" before _describe_ or "i" before _it_, it will run only this specific test and skip the others? 

```
ddescribe('my beautiful function', function() {
 iit('having fun', function() {

 });
});
```

This is especially helpful when you need to focus on debugging specific test.

Hope you liked it.
If you have more tips to share, please do.