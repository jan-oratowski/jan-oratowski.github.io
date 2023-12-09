---
layout: post
title: "Enabling custom package sources in Synology DSM 7.1 and 7.2"
date: 2023-10-20 23:15:00 +0100
categories: Synology DSM community
---

I have no complaints about packages provided by default Synology feed. They are fine and let me do most of the stuff I need want to do with a NAS.

Unfortunately sometimes I need something that is not included in the default feed.

One solution would be to download binaries / compile them myself every time I need something, but it gets tedious really fast and updating it later will be even worse.

Fortunately, it's possible to add additional package sources to DSM.

To do it go to `Package Center`, click on `Settings`, then `Package Sources`.

![2023 10 20 synology custom package sources](https://oratowski.com/assets/images/2023-10-20-synology-custom-package-sources.png)

Here you can add custom feeds to package sources. For example I use [SynoCommunity](https://synocommunity.com/) (feed address: `https://packages.synocommunity.com/`) which has a bunch of useful stuff like Syncthing, or Transmission.

