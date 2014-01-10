---
layout: post
title: A Case For XCode Snippets and Version Control
tags:
  - xcode
  - git
comments: true
published: true
---


##What's The Problem?
Cocoa is incredibly verbose. While this can make reading it self explanatory, it can also make writing it laborious. Even with code completion, I still find myself having to look up the documentation just to remember what I even need to code complete. It doesn't matter how many times I wire up a UITableView data source & delegate, I can never remember it all. 

I mean, who wants to type (or copy & paste) this every time:
{% highlight objectivec linenos=table %}
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
	NSString *identifier = @"myCell";
	UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:identifier];
    if (!cell)
    {
        cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:identifier];
    }    
    cell.textLabel.text = @"Cell";    
    return cell;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
	return 0;
}

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
	return 0;
}

- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section {
	return @"Header";
}
{% endhighlight %}


Cue [Xcode Snippets](https://developer.apple.com/library/ios/recipes/xcode_help-source_editor/CreatingaCustomCodeSnippet/CreatingaCustomCodeSnippet.html)! 

##What Are Code Snippets?
Code snippets are a kind of custom defined code completion. You, the coder, can define a custom shortcut for a longer bit of code. These are especially great for Cocoa APIs, which often require many wordy method implementations.

A couple of fantastic features:

* Symbolic <# placeholders #> can be used to quickly tab through and supply text that will vary each time the snippet is used.
* Completion Scope can be specified. This prevents class level snippets from being suggested when your cursor is inside of a method.

![Xcode Snippet Edit Dialog](/assets/img/xcode_snippet.png "Xcode Snippet")

##Why Use Them?
Because they save time. Sometimes they save lots of time. I'm personally not one to pour over the number of keystrokes required for every task, but, in the case of Cocoa, we're talking about saving much more than keystrokes. Loading up documentation, searching for the right class or protocol, and then finding the method signatures I need can be a significant time sink when done dozens of times per day. 

It takes time to get into the habit of using them. Defining them is easy, but using them is often hard to remember. Generally, I double check my list of snippets once every couple of months. If I don't use them, it's generally because they're not long enough to save me much time so they go into the garbage.

One of my favorite snippets (because I can never seem to remember it): Singleton using GCD
{% highlight objectivec linenos=table %}
+ (instancetype)shared<#name#> {
    static <#class#> *_shared<#name#> = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _shared<#name#> = <#initializer#>;
    });
    
    return _shared<#name#>;
}
{% endhighlight %}


##Now Go Curate and Save Them
If you start spending time refining your user defined snippets and really begin relying on them, you certainly don't want to lose them. The best way to back them up is to put them under version control, of course!

As of Xcode 4/5, they reside here: 
 
{% highlight bash %}
~/Library/Developer/Xcode/UserData/CodeSnippets
{% endhighlight %}

Unfortunately, the file names are not very friendly - they're GUIDs. I've seen some [manual solutions](https://github.com/brennanMKE/XcodeCodeSnippets) for "installing" snippets from human readable files, but I really just need a personal backup of these snippets. Friendly named or readable files would be great for public discoverability, though. 

##Where to Start?
Have your own code snippets?

{% highlight bash linenos=table %}
 cd ~/Library/Developer/Xcode/UserData/CodeSnippets
 git init
 git commit -a -m "Initial commit"

 *setup your remote repo*
 git push origin master
{% endhighlight %}

Need some snippets to start with? You could [try mine](https://github.com/sethgho/xcode-snippets), which are largely derived from [Matt Thompson's](https://github.com/mattt/Xcode-Snippets).
