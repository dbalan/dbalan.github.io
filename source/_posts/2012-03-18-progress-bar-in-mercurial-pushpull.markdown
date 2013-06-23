---
author: dhananjayishere
comments: true
date: 2012-03-18 02:56:00
layout: post
slug: progress-bar-in-mercurial-pushpull
title: Progress bar in mercurial push/pull
wordpress_id: 112432788
categories:
- Free software
- Programing
- Revision Control
---

I admit I am a huge Git fanatic. Infact I havent used anything else for managing the code (except some checkout from svn). I was trying to build [orange](http://orange.biolab.si/), so I wasnt very happy when I realised they use [mercurial](http://mercurial.selenic.com/wiki/Mercurial) for the revision control (I, like all my fellow programmers is a lazy person to adapt ;-) ).

 The first problem I faced was when cloning the code (checkout, subversion guys!), by default mecurial doesnt give you any progress dialogs. It can get frustrating if you are cloning a substantially large repository.
Good thing is mercurial from 1.5 onwards contains an extensoin for doing this, called [progress](http://mercurial.selenic.com/wiki/ProgressExtension). Only thng is you have to enable it explicitly.

Note that as per the mercurial documentation,system wide hg configuration file is stored in any of the following paths,



```
(Unix) /etc/mercurial/hgrc
or
 /etc/mercurial/hgrc.d/*.rc
(Windows) Mercurial.ini or(Windows) hgrc.d*.rc
or
 HKEY_LOCAL_MACHINESOFTWAREMercurial
```
and repositroy specific configuration in

```
/.hg/hgrc [ from man hgrc ]
```

To enable the progress extention, Create the file if it doesnt exist and add the fllowing to it.
```
[extensions]progress =
```
This enables the progress extention. You can define the configuration specific to this extention, by creating a sperate section in hgrc named [progress]. Information about thease options can be obtained by executing



```
[dhananjay@dlab orange]$ hg help progress|head

progress extension - show progress bars for some actionsThis extension uses the progress information logged by hg commands to drawprogress bars that are as informative as possible. Some progress bars onlyoffer indeterminate information, while others have a definite end point...
```
For example if you want a progress bar with refresh time 05 second, your hgrc should be like this,

```
[dhananjay@dlab orange]$ cat ~/.hgrc
[extensions]
progress =

[progress]
refresh = 0.5
```

Note: This blog is heavily inspired from [http://stackoverflow.com/questions/308491/show-progress-of-mercurial-push-pull](http://stackoverflow.com/questions/308491/show-progress-of-mercurial-push-pull).
