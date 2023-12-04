---
layout: post
title: "Favicon with GitHub Pages, Jekyll and Minima theme"
date: 2023-12-04 10:19:00 +0100
categories: Web GitHub Pages
---
Recently I wanted to add a favicon to my GitHub page and to my surprise finding documentation on how to do that was quite difficult.

In the end I had to search at least few StackOverflow answers, and yet some of which despite being marked as answers didn't work as expected.

Get yourself an image you want to use as a favicon and save it as PNG. I named mine `favicon.png` and saved it in the root folder of my site. If you want you can save it in assets/images/, or any other place.

Favicon can't be added to the page with markdown. It has to be added in pure html, which means modifying the underlying template. The template I'm using is called Minima and I want to modify it by just modifying the header.

First I went to: https://github.com/jekyll/minima/blob/2.5-stable/_includes/head.html, downloaded the file, created `_includes` directory in the root of my working folder and placed the file there. Now Jekyll/GitHub Pages will use this file instead of the one in the template.

Modify the file by adding `<link rel="shortcut icon" type="image/png" href="{{ site.baseurl }}/favicon.png">` there.

This is how my file looks after that:

{% highlight html %}
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  {%- seo -%}
  <link rel="stylesheet" href="{{ "/assets/main.css" | relative_url }}">
  {%- feed_meta -%}
  {%- if jekyll.environment == 'production' and site.google_analytics -%}
    {%- include google-analytics.html -%}
  {%- endif -%}

<link rel="shortcut icon" type="image/png" href="{{ site.baseurl }}/favicon.png">
</head>
{% endhighlight %}

And I also went to `_config.yml` and added `jekyll-seo-tag` plugin.

It looks like that now:

{% highlight yaml %}
# Build settings
theme: minima
plugins:
  - jekyll-feed
  - jekyll-seo-tag
{% endhighlight %}

Deployed after that and so far it works fine.