---
layout: post
title: "Fixing fleet-server error when enrolling Elastic Agent"
date: 2023-12-11 12:00:00 +0100
categories: elastic agent fleet server fix
---

Since I needed some logs from app running on-prem, I've asked a colleague to install Elastic Agent on one of our Windows Servers.

Unfortunately he came back to me with that error:

![2023 12 11 agent error](https://oratowski.com/assets/images/2023-12-11-agent-error.png)

I was puzzled. Credentials were good (I copy-pasted them from `Add Agent` window), so I tried running it on my computer and got the same error.

Then I tried accessing the resource URL and got this:  

{% highlight json %}
{
    "ok": false,
    "message": "Unknown resource."
}
{% endhighlight %}

It took me a while to figure out what was happening, but finally went to the list of [deployments](https://cloud.elastic.co/home), clicked on Manage, then on the left selected Activity and found this:

![2023 12 11 agent error 2](https://oratowski.com/assets/images/2023-12-11-agent-error-2.png)

Looks like the instance I wanted to use was correctly deployed with `Fleet`, but it later was automatically uninstalled.

To install it I selected `Edit` on the left and then under `APM & Fleet` clicked `+ Add capacity`.

![2023 12 11 agent error 4](https://oratowski.com/assets/images/2023-12-11-agent-error-4.png)

After few minutes it got deployed and now looks like that:

![2023 12 11 agent error 3](https://oratowski.com/assets/images/2023-12-11-agent-error-3.png)

I have re-tried installing the Elastic Agent and this time it succeeded.