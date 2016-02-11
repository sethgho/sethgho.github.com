---
layout: post
title: Introducing RxSplit
tags:
  - android
  - rxjava
comments: true
published: false
---

I copy this class into all the little apps I make. I'm tired of doing it. Now it's a library!

## Usage

1. Add the dependency: `compile com.sethgholson:rxsplit:0.1`
1. Define your own implementation of `Splitter`.
1. Build an instance: 
	- `RxSplit rxSplit = RxSplit.newBuilder().splitter(yourSplitter).build();`
1. Use that instance everywhere you need to translate your Strings to Observable streams!

It's that easy!

__NOTE__: It's on you, the client, to determine how exactly to split the Strings. That is beyond the scope of RxSplit. In an effort to keep this library lightweight and focused, it's up to you to figure out how exactly you want to split the Strings.

__P.S.__: This is a dumb. Don't use this.