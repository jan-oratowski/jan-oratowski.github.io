---
layout: post
title: "Get APN certificate EndDate in C#"
date: 2024-01-09 10:00:00 +0100
categories: apple push certificate
---

We have some Apple apnsCertificates used for Push Messages. They are only valid for a specific amount of time and have to be renewed.

Since our users should renew those certificates by themselves, but they usually forget about it, one of my colleagues wanted to set up a reminder for them.

One way to do that would be to set up an automatic reminder that will send message to everyone X days after the certificate has been uploaded.

But this looked like something that can easily go out of sync, so instead we wanted to check for expiring certificates every day.

As a proof of concept I set up simple script in LinqPad:

{% highlight c# %}
var base64 = "cert goes here";

var bytes =  System.Convert.FromBase64String(base64);

var cert = new X509Certificate2(bytes);

cert.NotAfter.Dump();
{% endhighlight %}

Now you just have to put it into some Azure Function or some other app that will be periodically run by a cron job and make it send notifications based on cert expiry date. 
