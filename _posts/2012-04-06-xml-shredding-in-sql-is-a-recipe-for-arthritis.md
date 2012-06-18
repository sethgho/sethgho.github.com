---
layout: post
title: 'XML Shredding In SQL Is A Recipe For Arthritis'
category: Coding
tags:
  - xml
  - sql
  - csharp
comments: true
---

At work I've been spending a lot of time the past couple of weeks doing the same thing: serialize the records in a table as XML, pass it up to the client, then back down to another database to be deserialized and merged. It's nothing fancy, but it's certainly tedious. It's generally been a pattern of:

Generate the XML: (easy)
<script src="https://gist.github.com/e59d1cfe037e3c18648b.js"></script>

To create something like this:
<div class="well">&lt;Root&gt;
&lt;Foo Column1="Value1" Column2="Value2" Column3="Value3" Column4="Value4" Column5="Value5" /&gt;
&lt;/Root&gt;</div>
But having to type this out has been the arthritic step. For larger tables, this can take a while.

<script src="https://gist.github.com/d64691b41a956ca67431.js"></script>
I know of nothing to automatically generate something like this, and yesterday I decided enough is enough (after coming to a table that was 65 columns wide). I wanted a way to quickly write the SELECT clause of something like this for me. Quick and easy was important, because if it were a chore to use I'd likely just write it out, grumbling the whole time.

The table definition is easy to generate via Management Studio. Right Click the window &gt; Script Table As &gt; Create To &gt; New Query Window and you get something like:
<script src="https://gist.github.com/8851019430fce999ee21.js"></script>

I settled on using the clipboard as the medium so I don't need to deal with saving a file or using a form for input. With this pinned to my taskbar, I just copy the table definition text to my clipboard and click the icon. Voila! The result is ready to be pasted. There's nothing fancy here. Just convenience.
<script src="https://gist.github.com/2323419.js"></script>

Oh, and if this is crappy, <a title="fork it and fix it on gist." href="https://gist.github.com/2323419" target="_blank">fork and fix it on gist</a>.
