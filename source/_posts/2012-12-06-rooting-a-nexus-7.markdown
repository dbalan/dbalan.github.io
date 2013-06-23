---
author: dhananjayishere
comments: true
date: 2012-12-06 18:26:00
layout: post
slug: rooting-a-nexus-7
title: Rooting a nexus 7
wordpress_id: 171074083
categories:
- Android
- Programing
- Hack
- Rooting
---

Lot of posts in the web about this is just bogus, all of them want you
to download a fat rootkit and click on the root.exe :-/

Being a developer device, rooting nexus 7 is easy.

1. Gain developer privilege (figure out yourself :-P)
2. Reboot to bootloader
```
$ adb reboot bootloader
```
3. Unlock the bootloader
```
$ fastboot oem unlock # Might have to be the superuser.
```
4. Download the recovery image for device from [here](http://clockworkmod.com/rommanager)
and flash it
```
$ fastboot flash recovery
```
5. Get the [superuser binary](http://forum.xda-developers.com/showthread.php?t=1538053).
6. Reboot the device and put it in the sdcard (or any storage you have,)
7. Reboot to the recovery and flash it.
```
 $ adb reboot recovery
```


Note: People suggested using this to [keep root priviliges](https://play.google.com/store/apps/details?id=org.projectvoodoo.otarootkeeper&feature=search_result#?t=W251bGwsMSwxLDEsIm9yZy5wcm9qZWN0dm9vZG9vLm90YXJvb3RrZWVwZXIiXQ..) after OTA -
