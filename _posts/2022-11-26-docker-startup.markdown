---
layout: post
title:  "Changing docker startup options without re-creating container"
date:   2022-11-26 16:56:43 +0100
categories: docker startup options
---

## With command line

### If the container is running and you want to modify it's settings:

{% highlight bash %}
docker update --restart=<policy> <name>
{% endhighlight %}

### If the container is not running and you want to start it:

{% highlight bash %}
docker container run --restart=<policy> <name>
{% endhighlight %}

### Policy can be any of those:
 - no
 - always
 - unless-stopped
 - on-failure
 
## With docker-compose

It can be set in docker-compose file like that:

{% highlight yaml %}
version: "3"
services:
  app:
    image: linkace/linkace:simple
    restart: unless-stopped
{% endhighlight %}