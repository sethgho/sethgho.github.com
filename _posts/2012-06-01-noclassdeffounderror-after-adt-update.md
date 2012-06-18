---
layout: post
title: 'NoClassDefFoundError After ADT Update'
tags:
  - adt
  - android
comments: true
---

<p>I’ve just returned to an Android project after a couple of months’ pause. After updating Eclipse and ADT, my project started throwing an exception:</p>  <pre class="brush:java">06-12 21:45:26.154: ERROR/AndroidRuntime(3654): java.lang.NoClassDefFoundError: com.google.gson.gson</pre>

<p>This JAR file was clearly in my “lib” folder in the project and in my build path. After entirely too much fiddling about, cleaning, rebuilding, and googling, I discovered my problem. Apparently, ANT is now expecting these to be in the “libs” folder. After moving all of my third party JAR files from “lib” to “libs”, deleting “lib”, and restarting Eclipse, all is right the the world again!</p>
