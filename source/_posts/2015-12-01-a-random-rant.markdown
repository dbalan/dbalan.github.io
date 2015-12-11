---
layout: post
title: "A Random rant"
date: 2015-12-01 00:00
comments: false
categories:
- life
- rant
- filesystems
---

```
/me sets +rant
```
Yesterday, Found an old portable hard disk in the attic. Face lights up. Connect to computer, doesnt work. The connection probabaly fried. Its probabaly the connector, HDD internally uses a `SATA` bus.

I know what to do, lets oopen the server box and connect to the motherboard. Can’t find any SATA cable. `find sata ~house`

Finally hard disk plugged in, `FreeBSD` boots. `dmesg` shows everything is alright, except `ext4`. #sigh

Somebody suggests `fuse`. Alright, thats it then. Compile, `kldld` and booyeah!

Okay, its full of photos from past. Wow! I need to see them, lets share it to something with a monitor. That’d be my mac. `sshfs`? Sorry dude, you need the whole `XCode` suite and should sacrifice an extra kidney to load unsigned `kext`s.

But there are other ways of sharing files. `SMB` FTW!

Why the fuck are there three samba versions in ports. `cd /usr/ports/samba$(random_ver)`

Okay, samba is setup and mounted, tears

Nooo - I can’t access the hard disk. Why? huh perms fucking perms!

I got this! gonna chmod the shit out, but except… it doesn’t work. What the fuck does not implemented mean?

JFGI. JFGI POints to ext4 code - ext4 fuse is strictly read only. (facepalm)

Story still continues…
