---
layout: post
title: .NET WCF JSON DateTime Hell 
tags:
  - .net
  - json
comments: true
published: false
---

Scratch notes. Write something up later:

/Date(-335577600000+0000)/ produces a .NET DateTime of 5/15/1959 12:00 AM with a DateTimeKind of Local, so it's automatically being offset by 5 hours (CST in Daylight Savings Time).
/Date(-335577600000)/ produces a .NET DateTime of 5/15/1959 with a DateTimeKind of UTC, causing no automatic offset.

I was under the misunderstanding that +0000 is explicitly forcing it to be a UTC time. It's simply explicitly declaring it to be a kind of time that is local and in the UTC offset.
So if you explicitly want to pass up a UTC time, do not specify an offset.

In my case I needed to handle both for my current Android app and the existing iOS app which is incorrectly sending +0000, so in my DataContract's property:

private DateTime _dateOfBirth;
[DataMember]
public DateTime DateOfBirth 
{ 
	get
	{ 
		return _dateOfBirth; 
	} 
	set
	{
		_dateOfBirth = value.Kind == DateTimeKind.Utc ? value :
			DateTime.SpecifyKind(value.ToUniversalTime(),DateTimeKind.Utc);
	} 
}