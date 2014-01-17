---
layout: post
title: Cut the Cord: Debug Android Wirelessly
tags:
  - android
  - adb
comments: true
---

This is one of those "I've wanted it for so long I really don't want to forget this" posts. I'm taking a cue from [Scott Hanselman](http://www.hanselman.com) and writing a quick blog post about it so I remember.

To debug your Android app on a physical device without needing to keep the cord connected the whole time, it's really straight forward. First:


1.  Connect via usb.
2.  run: **adb tcpip 5555**
3.  Remove the phone from usb.
4.  Run **adb connect [device's wifi IP address]**

Now you can run **monitor** or **adb devices** and see that your device is connected! You can run builds directly on the device and debug as necessary.

Oh, mana from heaven! I don't know why this was such a mystery to me. I know I've googled for this kind of solution on at least two occasions, but I never landed on the [Android Developer Guide](http://developer.android.com/guide/topics/connectivity/usb/index.html) page that says exactly how to do accomplish this. Doh.

Thanks to [Pablo Costa Tirado](https://plus.google.com/+PabloCostaTirado/posts/aS7dARQE4bZ) for pointing this out on the [Android Developer Tools](https://plus.google.com/communities/114791428968349268860) community on Google Plus. 
