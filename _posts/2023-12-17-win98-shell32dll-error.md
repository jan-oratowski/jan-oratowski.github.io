---
layout: post
title: "Fixing Windows 98 shell32.dll error on modern hardware"
date: 2023-12-17 12:10:00 +0100
categories: windows9x VirtualBox shell32
---

Recently I tried to run Windows 98 in VirtualBox, but got this error:

> The SHELL32.DLL file is linked to missing export SHLWAPI.DLL:tFileAttributesA.


![2023 12 17 win98 shell32dll error](https://oratowski.com/assets/images/2023-12-17-win98-shell32dll-error.png)

What was puzzling is that this VM previously worked without any problems. I have run it successfully in VirtualBox few years ago and nothing has changed since the last run.

The only thing that has changed was the computer it was running on.

Previously it was Windows 10 on 3rd Gen i7, now it's Windows 11 on 4th Gen Ryzen.

Turns out this matters. There is a bug in Windows 95, 98 and ME that prevents those systems from running on new processors, even if it's being run inside the VM.

Fortunately there is a fix:

Download the latest release from this page:

[https://github.com/JHRobotics/patcher9x/releases](https://github.com/JHRobotics/patcher9x/releases)

I'm running already installed Win 98 SE in VirtualBox, so I need `patcher9x-0.8.50-boot.ima` file.

If you want to patch the installer, then use `patcher9x-0.8.50-win64.zip`.

Next I've went to settings of my VM and selected the floppy image downloaded in previous step.

![2023 12 17 win98 shell32dll error 2](https://oratowski.com/assets/images/2023-12-17-win98-shell32dll-error-2.png)

After booting the VM, it went straight to the floppy boot and DOS prompt, next I typed:

{% highlight dos %}
A:\> patch9x
{% endhighlight %}

Then selected:

`3 (patch both)`

Pressed `Y` to confirm and waited for it to finish.

I have ejected the floppy and did a reboot (by doing `CTRL+ALT+DEL`).

Fixed, no errors anymore. :)