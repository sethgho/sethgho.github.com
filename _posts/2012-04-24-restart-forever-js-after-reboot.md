---
layout: post
title: 'Restart Forever.js After Reboot'
category: Coding
tags:
  - bash
  - javascript
  - node-js
comments: true
---

I’m amid migrating from a Dreamhost shared server to a VPS. A benefit of this is the ability to have long running processes like node.js. I’m also migrating the back end for <a title="Praaaaaaaaaaaaaise the Looooooooooord it's Tuesday! Wait... Damn. It's Tuesday." href="http://itunes.apple.com/us/app/menu-line-george/id440761181" target="_blank">Menu Line George</a> to Parse.com. My v1 process for recording the George calls was a kludge of scripts running on my home desktop to call via Skype. This was more a proof-of-concept than a long term solution. Now I’ll be using <a href="http://www.twilio.com" target="_blank">Twilio</a> + <a title="I can't stand the taste of V8." href="http://www.nodejs.org" target="_blank">node.js</a> + <a title="Most ungooglable product name ever." href="http://www.parse.com" target="_blank">Parse</a> as my permanent solution, significantly reducing how much I’ll need to think about it on a daily basis.

The simplest way I’ve found to keep a node script running as a service is <a title="He got caved in, and he's been there ever since. Forever? Forever." href="https://github.com/nodejitsu/forever" target="_blank">forever.js</a>. If you’re new to node, I suggest checking it out. Otherwise, I’m sure you’ve heard of it.

I fired it up yesterday and it worked like a champ. That is, of course, until my VPS rebooted overnight for some reason and the call wasn’t made this morning. I found a handy little guide over at Hack Sparrow for creating a cron job to restart your node script with forever when the machine reboots.

First create a shell script like this one (I called mine <em>app-starter.sh</em>):

```bash
#!/bin/sh
 
if [ $(ps aux | grep $USER | grep node | grep -v grep | wc -l | tr -s "\n") -eq 0 ]
then
        export NODE_ENV=production
        export PATH=/usr/local/bin:$PATH
        forever start ~/example/app.js > /dev/null
fi
```

Then make the script executable:
{% highlight bash %}chmod 700 ~/app-starter.sh{% endhighlight %}
Now make cron run the script when the system is rebooted. Add this to your crontab (via <em>crontab –e</em>):
{% highlight bash %}@reboot ~/app-starter.sh &gt;&gt; cron.log 2&gt;&amp;1{% endhighlight %}
For the uninitiated like myself, use<em> CTRL+K,X</em> to save.

Thanks to Hack Sparrow for taking the time to share this.

via <a title="The night starts now" href="http://www.hacksparrow.com/make-forever-reboot-proof-with-cron.html" target="_blank">Hack Sparrow</a>.
