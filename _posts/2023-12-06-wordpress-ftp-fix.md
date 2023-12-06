---
layout: post
title: "Fixing wordpress asking for FTP credentials"
date: 2023-12-06 11:37:00 +0100
categories: FTP Web WordPress Linux
---
We run one of our marketing sites with WordPress. It's installed in a VM in Azure, however recently there was a problem when trying to install plugins.

The WordPress admin panel kept asking for an ftp connection details to install plugins.

## If you want to set up FTP

Install `proftpd` and `ftp` client (to check if it works).

{% highlight bash %}
apt install proftpd ftp
{% endhighlight %}

Now you can edit the config file in `/etc/proftpd/proftpd.conf` (not required).

To test if it works try connecting with your credentials:

{% highlight bash %}
ftp
open
127.0.0.1
your-username
your-password
{% endhighlight %}

If it works you can try issuing commands like `ls` and `cd` to navigate around, then `quit` when you're done.

Now you can provide those values in WordPress and it will use them whenever it needs to install/update plugins.

Since you're using `127.0.0.1` as the ftp server, nothing will travel through the network. This makes it quite secure.

You may want to block port `21` on your firewall, just to make sure nobody else can connect to it.

## Fix this without setting up FTP

I looked around a bit more and it turns out WordPress will ask for FTP credentials only if it can't modify files directly.

To check if files can/can't be modified, it will try to create a temporary file. If it fails, then it will swallow the exception and default to using FTP.

To prevent it from happening edit `wp-config.php` and add this line:

{% highlight php %}
define('FS_METHOD', 'direct');
{% endhighlight %}

Now if you try installing the plugin, it will give show you what is the issue. This will be something about not having write access to the path in which plugins are stored.

Fixing the permissions depends on the user your web server is running as and what type of installation you are using. If it's standard www-data, then:

{% highlight bash %}
chown -R www-data path-to-wordpress/wp-content
{% endhighlight %}

Some people report it doesn't work, but this one works: (this is definitely less secure)

{% highlight bash %}
chown -R www-data path-to-wordpress
{% endhighlight %}

Sometimes it's apache user:

{% highlight bash %}
chown -R apache:apache wordpress
chmod u+wrx wordpress/*
{% endhighlight %}

And some people just don't want to care about permissions, because it's a separate instance that runs only one WordPress site, so they do:

{% highlight bash %}
chmod -R 777 path-to-wordpress
{% endhighlight %}

That one will work for sure, however anyone who can login to the server will be able to modify/execute those files.