---
layout: post
title: OSX Terminal Shortcuts I Wish Young Me Knew
tags:
  - xcode
  - git
comments: true
published: true
---

I was reared in Microsoft's world. I only use the command prompt for running ipconfig, like every other red blooded American, right? A *nix terminal was a pretty foreign environment for me. For years I knew enough to explore & navigate a directory structure, but that's about it.

Now that I've been spending some time in OS X, I've become much more comfortable using the terminal. It continues to be a learning process, but I thought I'd list a few shortcuts that I suspect are so old and deeply rooted in *nix based environments, that everyone listing "Must Know Shortcuts" assumes they're already known. Well, I didn't know them.


##Moving the Cursor
=================

I first discovered this in a reply to [@climagic](https://twitter.com/climagic) on Twitter.


* Go To Beginning Of Line: __CTRL + A__
* Go To End Of line: __CTRL + E__

![Terminal Animation Beginning and Ending of Line](/assets/img/terminal_shortcut_bol_eol.gif "Terminal Animation Beginning and Ending of Line")


Now, these are pretty awful. These are OS X Terminal specific from what I can tell. Not that they are separated key presses, not simultaneous.



* Move Backwards 1 Word: __ESC, B__
* Move Forward 1 Word: __ESC, F__  

![Terminal Animation Beginning and Ending of Line](/assets/img/terminal_shortcut_words_esc.gif "Terminal Animation of Moving Forward & Back Words using Escape")

Fortunately, you can enable "[Use Option as meta key](http://stackoverflow.com/questions/81272/is-there-any-way-in-the-os-x-terminal-to-move-the-cursor-word-by-word#comment9413062_81309)" in your terminal preferences. This will allow you to pres *and hold* the option key, while pressing B and F to move backward and forward. Not great, but this is a step in a better direction.


* Move Backwards 1 Word: __ALT + B__
* Move Forward 1 Word: __ALT + F__  

![Terminal Animation Forward and Ending of Line Using Option](/assets/img/terminal_shortcut_words_alt.gif "Terminal Animation of Moving Forward & Back Words using Option")

*__Note__: the on screen keyboard is showing a crazy key combo - I suspect this has something to do with the preference override.*


##Editing
=================

* Undo!: __CTRL + ___
* Backspace word: __ALT + Backspace__
* Backspace entire line: __CTRL + U__
* Delete word: __ALT + D__ <- Particularly useful on a macbook keyboard with no (forward) delete key.

  
  
While certainly not exhaustive, these are the shortcuts I found invaluable and immediately started using as soon as I discovered them. For a more complete list, including history navigation, head over to this [ss64.com link](http://ss64.com/osx/syntax-bashkeyboard.html).