---
layout: post
title: "Fixing huge .git directory"
date: 2023-11-11 12:10:00 +0100
categories: git windows linux build cleanup
---

Recently build tasks started failing. Turned out there was not enough free space on the drive.

After quick check, I've noticed that the `.git` directory was 100 times bigger than the whole repo.

This was caused by some orphaned objects and other garbage pilling up and never being deleted.

I just run opened command prompt and run:

{% highlight bat %}
git gc
{% endhighlight %}

That fixed space issue - I've managed to get back around 40GB of drive space.

[Docs for "git sc"](https://git-scm.com/docs/git-gc).