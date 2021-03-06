---
layout: post
title: 'SSMS “Connect to Database Engine” Prompt Every Time A Saved Query Is Opened'
category: Coding
comments: true
tags:
  - sql
  - ssms
---

<p>About two weeks ago, I noticed Sql Server Management Studio’s behavior changed on me. I often use saved <img title="SSMS screenshot" border="0" alt="SSMS screenshot" align="right" src="/assets/img/ssms_connect.png" width="301" height="228" />queries for deployment, so I’m saving/opening them all day long. For as long as I’ve been using SSMS, it has <em>always</em> just used my existing connection in Object Explorer as the connection context for the saved file. Something changed, and I now have to react to this dialog <em>every time I open a file.</em> It doesn’t matter if I have a connection established in object explorer or not. </p>  <p>My irritation level finally rose to the point this morning that I decided to address it. I’d given Googling it a solid 25-35 minutes worth of effort before I decided to bother anyone else about it. All I saw were people complaining of the same problem with no real solutions. Most of the responses were justifications for the new behavior, but they just didn’t seem to get the OP’s problem: The behavior used to be different! Something changed!</p>  <p><a title="Mr. Anderson" href="http://pirootofpi.com/" target="_blank">Dave’s</a> installation was acting exactly like mine used to – the way I want it to. <a title="He just got an iPhone 4. Jealous." href="http://www.chrisbenard.net" target="_blank">Chris Benard</a> simply “rarely uses saved queries.” Has anyone ever experienced this and know the solution? It’s driving me nuts!</p>
