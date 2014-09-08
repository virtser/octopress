---
layout: post
title: "Live page reload"
date: 2014-09-08 10:04
comments: true
published: true
---
If you are working with Sublime Text 2/3 and you want to be able to see live changes on your HTML/CSS layout, follow the steps below:

1. Find and install a new package from [SublimeText](http://www.sublimetext.com/3) called "LiveReload". Set ```"save_on_focus_lost" :true``` in user settings to enable auto save functionality.

2. Add [LiveReload Chrome extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei) which you will have to enable in order to activate LiveRecord on page you are working at. Make sure to select in extensions management screen " Allow access to file URLs" to enable this functionality on local files as well. 

3. Install and run free [livereload node.js server](https://github.com/napcs/node-livereload) by running the following terminal commands:

```
$ npm install -g livereload
$ livereload [path]
```