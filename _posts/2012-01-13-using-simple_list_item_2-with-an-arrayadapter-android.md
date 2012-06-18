---
layout: post
title: 'Using simple_list_item_2 with an ArrayAdapter (Android)'
tags:
  - android
  - java
  - xml
comments: true
---

Today I wanted to display static a ListView of properties and their values. It’s Friday, so I really wanted to do this with as little work as possible. Android’s free layout simple_list_item_2 sounded like what I wanted, but it wasn’t immediately clear how to handle this. There are a lot of lazy ways we can list single values, but Googling around how to use simple_list_item_2 resulted in lots of questions with no real answer.

I found Mark Assad, who parsed the system layout files into <a href="http://sydney.edu.au/engineering/it/~massad/project-android.html" target="_blank">raw XML</a>. The led to the magic answer of <a href="http://developer.android.com/reference/android/widget/TwoLineListItem.html" target="_blank">TwoLineListItem</a> widget. Finding this widget allowed me to write a simple ArrayAdapter of key/value pairs.

<script src="https://gist.github.com/ff754ed165c6e4c26cd6.js"></script>
Hope this saves someone else some time, as I spent an embarrassing amount of time determined to use the simple_list_item_2 layout.
