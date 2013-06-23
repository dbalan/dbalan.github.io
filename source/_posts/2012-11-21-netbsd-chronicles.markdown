---
author: dhananjayishere
comments: true
date: 2012-11-21 21:45:00
layout: post
slug: netbsd-chronicles
title: NetBSD Chronicles.
wordpress_id: 169330104
categories: NetBSD
---

To be frank I wasn't doing much for almost an year, got lazy as one can ever be. Today was the day to break it. Got a little push do something and I got down to do it. I was looking at BSD development for a long time, and thought this is the best time to get involved. I am a total noob at BSD, I never really used one. So it was challenging when I started to install NetBSD into an old Comapq nx6120 that was lying around. I know anyone could get to the root shell easily, with help from brilliant click and go installers, configuring and customizing was the real problem.

Its 0300 now, and I got my laptop running NetBSD 6.0, and connected to wireless (easier than I thought - thanks to legacy hardware.)

**Configuring Intel PRO/Wireless **

** **Unlike linux, BSD can include all the microcode (firmware) in the distribution itself, due the flexibility of licensing system. Reading up _iwi(4)_ reveals youve to accept the EULA by setting the sysctl variable hw.iwi.accept_eula to 1

```
# sysctl -w hw.iwi.accept_eula=1
```

The university wireless is open, so I didnt had to mess too much.

```
# ifconfig ssid "SSID" iwi0 dhclient iwi0
```