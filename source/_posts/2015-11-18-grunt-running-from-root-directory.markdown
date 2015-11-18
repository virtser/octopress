---
layout: post
title: "Grunt running from root directory"
date: 2015-11-18 21:46
comments: true
published: true
---

![](http://gruntjs.com/img/grunt-logo.png)

If you are a web developer and you are using [Grunt](http://gruntjs.com/) as your default task runner, you probably in most of the cases use it from some inner folder of the project, something like "*client/app*".

In this case, every time you want to work on your code using command like "*grunt serve*", you need to change directory into *client/app* to run it all the time.

Below, I show you the way to make grunt commands work from root directory which makes your life more comfortable, eliminating the need switching to *client/app* directory all the time.


1. Add in your original *client/app/Gruntfile.js* file the following code to let Grunt know the base directory location:
 
```
module.exports = function(grunt) {
  // Must have in order to work from root
  grunt.file.setBase(__dirname);

	...

}
```

2.. Add symbolic link in your root directory to original *client/app/Gruntfile.js* file:

```
ln -s client/app/Gruntfile.js Gruntfile.js
```

3.. Create *package.json* in root directory with grunt as dependency and install Grunt:

```
npm init
npm install grunt --save-dev
```
4.. Run grunt from root to test it.

```
grunt serve
```


That's it, pretty simple.
Hope you like it and use it.