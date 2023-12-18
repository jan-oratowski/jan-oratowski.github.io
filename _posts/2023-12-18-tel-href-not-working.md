---
layout: post
title: "Tel: not being rendered in Razor Pages"
date: 2023-12-18 12:16:00 +0100
categories: tel href razor c# dotnet Ganss htmlsanitizer
---

Some of our customers like adding `tel:` to `a href tags`. This way people can phone them by clicking on links. 

Recently they've complained that those tags stopped working.

I navigated to the page, and it turned out the link in rendered Razor page has no target:

![2023 12 18 tel href not working](https://oratowski.com/assets/images/2023-12-18-tel-href-not-working.png)

After some digging I've found out we use: `Ganss.XSS.HtmlSanitizer`. In the code we initialize it with:

{% highlight c# %}
private static HtmlSanitizer _htmlSanitizerWithTags => new HtmlSanitizer(
             allowedAttributes: DefaultAllowedAttributes,
			 allowedTags: AllowedTagsWithIframe,
             allowedSchemes: AllowedSchemas);
{% endhighlight %}

The sanitizer is created with allowedSchemes property that contains what can be put into `a href` tag. It's as "easy" as "just" adding `tel` to the list of allowed schemas:

{% highlight c# %}
private static ISet<string> AllowedSchemas
        {
            get
            {
                var allowedSchemas = new HashSet<string>(HtmlSanitizer.DefaultAllowedSchemes);
                allowedSchemas.Add("mailto");
                allowedSchemas.Add("tel");
                return allowedSchemas;
            }
        }</string></string>
{% endhighlight %}