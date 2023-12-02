---
layout: post
title: "Limiting memory used by WSL2 and Docker on Windows"
date: 2023-12-01 12:59:01 +0100
categories: WSL2 Windows Docker Linux
---

> If you just want the answer without reading the whole page, [then just click this link](#how-to-do-it).

## (not so) short background

Whenever I buy a new computer, I always check how much RAM it can take, then try to buy as much RAM as possible.

In my mind this "RAM greed" is justified. I want to have as much stuff cached in-memory, so load times are as fast as possible.

I did the same with my newest work laptop, which has 64GB of RAM right now.

On average day it barely hits 32GB RAM used, but it's OK as I like to have a buffer.

Recently I've noticed that the RAM usage jumped to ~60GB. Quick check suggested it may have something to do with Docker Desktop. Although I have shut down most of the Docker containers, RAM usage was still pretty high.

On one hand, I still had plenty of RAM, so no harm done. On the other, it was bugging me, so I decided to figure out how to prevent Docker Desktop from using up all my free memory.

## what to do

Since Docker Desktop runs in WSL2, it's actually quite easy to set max RAM and CPU usage.

Most of the guides around the internet suggested editing `.wslconfig` file that should be in the `C:\Users\yourname` directory.

Turns out this file does exist on Windows 10, but isn't there on Windows 11.

Confusing. Fortunately it doesn't matter, as it can be created and will be read by WSL2.

## how to do it

Open notepad and create a new file that looks like this:  
  
*(obviously change those values to something that suits your needs)*

{% highlight ini %}
[wsl2]
memory=16GB
processors=8
{% endhighlight %}

Now click "Save as..." and paste there `%USERPROFILE%\.wslconfig`, then restart WSL2 (restart the service or restart your PC).

`%USERPROFILE%` is a path variable and Windows understands you want to go to your User folder.