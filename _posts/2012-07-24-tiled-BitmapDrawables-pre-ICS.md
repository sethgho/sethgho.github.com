---
layout: post
title: Tiled ActionBar Background in Android Prior To ICS
tags:
  - android
  - java
  - xml
comments: true
published: false
---

Trying to prettify an Android app with any kind of image assets has proven to be a bit of a challenge. I'm using the excellent [ActionBarSherlock](http://www.actionbarsherlock.com "I dont't get the name") to handle the ActionBar for OS versions prior to ICS. 

It's certainly made life much easier, but styling it left me wanting. I tried setting the Action Bar's background to a tiled image drawable: 
<script src="https://gist.github.com/3169855.js"> </script>

But the repeating attribute seem to have not been recognized at all. According to [this bug report](http://code.google.com/p/android/issues/detail?id=15340 "Android bug? no!") it's a problem with pre-ICS Android. The tile mode must be set in code and is not supported in the XML declaration. Example:

<script src="https://gist.github.com/3169765.js"> </script>

If anyone knows a better way to handle this, I'd love to know. I'm growingly increasingly hesitant to add any images anywhere in an Android project if I can avoid it.