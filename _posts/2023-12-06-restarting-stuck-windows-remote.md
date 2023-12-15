---
layout: post
title: "Restarting stuck Windows machine over Remote Desktop"
date: 2023-12-06 9:39:00 +0100
categories: Remote Windows Restart
---
In my job we use on-prem DevOps Agents for building our applications.

Recently one of those computers started acting weird. Seemed like the easiest way to fix it would be to restart the server.

Someone connected via Remote Desktop to it and issued the reboot. First nothing happened, then it was impossible to log-in via Remote Desktop, however VSTS Agent was still working OK.

Since nobody wanted to go to the closet in which we keep those computers, we just left it like that overnight because "maybe it will fix itself". Not only it didn't, but next day builds stopped working on this computer, so something had to be done.

As stated before - nobody felt like going to the computer and manually restarting it (with a button).

In this case it was pure laziness, however that's not always the case. Sometimes everyone is working from home and it may happen, or it can be a computer in some remote data center. In both of those cases ability to remotely troubleshoot and fix the restart may be useful and this is why I wanted to investigate how to fix it.

## Things to try first

My first attempt was to login there via RDP and try starting Task Manager, I was able to login far enough to see the black screen (so no desktop, or explorer), but was not able to start Task Manager (CTRL+ALT+DEL/INSERT didn't work).

Next I tried to connect with PowerShell.

It worked and I was able to run `shutdown /r`.

It complained that there was another restart in progress, so I tried `shutdown /a` to abort it, but it was impossible to abort the restart.

This sometimes happens when the shutdown process is stuck on `winlogon` process that for some reason can't be killed.

You can try to kill winlogon from PowerShell, with `Taskkill /IM "winlogon.exe" /F`.

In my case it complained that this process can't be killed.

There is a tool from SysInternals that will help you to "fix" that.

## Solution

Download  [PsTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools), unpack it somewhere and run:

{% highlight dos %}
pskill \\remote.computer.name winlogon
{% endhighlight %}

You can also specify credentials that should be used for the connection like that:

{% highlight dos %}
pskill \\hostname -u Administrator -p Password123 winlogon
{% endhighlight %}

This should do the trick.

The restart will either continue, or will be aborted and you will have to execute `shutdown /r` again, however this time it will complete.