---
layout: post
title: "Setup 2 PiHole servers and keep them in sync"
date: 2023-10-05 9:12:38 +0100
categories: pihole dual setup sync
---
Setup with one PiHole is good enough for most of the users, however my whole house runs on PiHole (including the DHCP server), so I need something that will work, even if the Pi goes down.

First I've installed two PiHole servers. In my case one is running on old Pi1B, another in LXC in Proxmox. That means they don't even need to be running the same architecture.

If you want PiHole to run as DHCP server

I want them to serve as DHCP servers, so I enabled the DHCP servers in two interfaces (pihole1 and pihole2), but set DHCP range to something else.

In my case I set it to:
 - pihole1: `192.168.178.100` - `192.168.178.149`
 - pihole2: `192.168.178.150` - `192.168.178.200`
 
This way each client will get the IP from any of those DHCP servers and there will be no conflicts in IPs assigned.

I also have some static IPs assigned from the range `192.168.178.2` - `192.168.178.99`, but I don't have to worry about them as they will be synchronized.

There is one more thing to do, I had to login to each of the piholes and execute:

{% highlight bash %}
sudo nano /etc/dnsmasq.d/99-second-DNS.conf
{% endhighlight %}

Add there this line (it will tell DHCP server to send those 2 DNS servers):

{% highlight conf %}
dhcp-option=option:dns-server,192.168.178.253,192.168.178.254
{% endhighlight %}

Then close nano and do:

{% highlight bash %}
sudo pihole restartdns
{% endhighlight %}

Synchronization

There are multiple options. One of them is GravitySync which works fine, but seems to be more CPU and storage intensive than what I want my Raspberry Pi 1 to go through. So I use OrbitalSync instead, it's easy to setup and requires one docker-compose file:

{% highlight yaml %}
version: '3'
services:
  orbital-sync:
    image: mattwebbio/orbital-sync:1
    environment:
      PRIMARY_HOST_BASE_URL: 'http://192.168.178.253'
      PRIMARY_HOST_PASSWORD: 'password1'
      SECONDARY_HOST_1_BASE_URL: 'http://192.168.178.254'
      SECONDARY_HOST_1_PASSWORD: 'password2'
      INTERVAL_MINUTES: 30
{% endhighlight %}

After deployed, the container will sync settings (including DHCP leases, whitelists, etc.) every 30 minutes.