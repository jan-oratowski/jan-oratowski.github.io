---
layout: post
title: "Replace part of text in a column in MySql/MariaDB database"
date: 2023-01-03 12:37:00 +0100
categories: MySql MariaDB replace
---

You can replace part of the text like that:

{% highlight sql %}
UPDATE Episodes  SET LocalFile = REPLACE(LocalFile, 'somethingOld', 'somethingNew')
{% endhighlight %}

Be carefull. It has no `WHERE` so will run on the whole table.