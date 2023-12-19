---
layout: post
title: "Fixing Cloudflare DNS + Azure AppService"
date: 2023-12-19 12:16:00 +0100
categories: cloudflare appservice azure dns fixing
---

Configuring Cloudflare DNS + proxy + Azure AppService isn't very complicated, but sometimes it doesn't work as expected. Some of the domains are managed in our Cloudflare account and some are managed by clients, which makes troubleshooting even more difficult.

Recently I discovered there is an automatic tool that will help with fixing those issues.

It's under AppService > Custom domains > Troubleshoot. From what I understand, it tries to analyze the logs and then shows what and how should be fixed.

![Custom domains troubleshooter](https://oratowski.com/assets/images/2023-12-19-fixing-cloudflare-azure-appservice.png)