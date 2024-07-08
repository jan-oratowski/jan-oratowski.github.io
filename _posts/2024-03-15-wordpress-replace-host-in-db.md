---
layout: post
title: "Replace references to old host in Wordpress (whole database)"
date: 2024-03-15 14:00:00 +0100
categories: worpress host replace notepad++
---

This post isn't about changing WordPress configuration. To do that please see my other post.

When you decide to change your site's URL, you may notice that all the previous post you made will still reference the old URL.

This may happen after cloning your site, or after restoring it to different hosting provider as well.

The "easy fix" is to run the query that will replace it in every column of every table. Doesn't look that "easy" to me.

What I've ended up doing is:
* export the whole database as one text file
* open in notepad++ and run find & replace on it - that replaced all instances of the old URL, but took some time, maybe better to do with some other utility?
* restore backup from the exported & modified file

