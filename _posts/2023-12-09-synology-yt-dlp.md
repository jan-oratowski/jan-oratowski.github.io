---
layout: post
title: "Installing yt-dlp (better youtube-dl) on Synology NAS"
date: 2023-12-09 2:10:00 +0100
categories: Synology DSM community yt-dlp youtube-dl
---

Sometimes I download a video or two from youtube or some other website to store it on my NAS for later.

Up till now I was using one of my computers to download and then send it via network to the NAS, but this process can be optimized to use NAS for everything.

At first I wanted to download 64-bit linux build of `yt-dlp` from GitHub, but when trying to run it I got some strange error about `libpython3.10.so` missing (although I had python 3.10 installed).

It seems that the more reasonable (and working) approach is to use pip and install `yt-dlp` with it.

You can install pip and `yt-dlp` when using Python 3.9 provided by Synology, however I had to run all the commands with `sudo`. Whenever I wanted to run `yt-dlp`, I also had to use `sudo` and it made me uncomfortable, fortunately using python provided by SynoCommunity solves this issue.

If you want to install SynoCommunity feed you have to follow this guide.

After that go to Package Center and click on Community - there are several python packages to choose from.

![2023 12 08 synology yt dlp](https://oratowski.com/assets/images/2023-12-08-synology-yt-dlp.png)

Now ssh into Synology and start by installing pip, then installing `yt-dlp`.

I have installed python 3.10 from SynoCommunity and python 3.9 from Synology, so I have to specify the version I want to use:

{% highlight bash %}
python3.10 -m ensurepip

python3.10 -m pip install -U yt-dlp
{% endhighlight %}

If you use python provided by Synology and get an error, it means you have to use `sudo`.

If you use python provided by SynoCommunity, you will get a warning about bin folder not being included in your `$PATH`.

To fix that edit `~/.bashrc` (if it doesn't exist just create it)

{% highlight bash %}
nano -w ~/.bashrc
{% endhighlight %}

And add this line:

{% highlight bash %}
export PATH=$PATH:$HOME/.local/bin
{% endhighlight %}

Close nano (by pressing `CTRL+X`, then `Y` to save the changes) and run the same command in the terminal:

{% highlight bash %}
export PATH=$PATH:$HOME/.local/bin
{% endhighlight %}

Now you can check if the `$PATH` has been updated by doing:

{% highlight bash %}
echo $PATH
{% endhighlight %}

And now it's possible to run `yt-dlp` with:

{% highlight bash %}
yt-dlp
{% endhighlight %}

If you installed `yt-dlp` first with python from Synology and now with python from SynoCommunity, you should uninstall the previous `yt-dlp` installation by doing:

{% highlight bash %}
sudo python3 -m pip uninstall yt-dlp
{% endhighlight %}