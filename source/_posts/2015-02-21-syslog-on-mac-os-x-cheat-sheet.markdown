---
layout: post
title: "Syslog on Mac OS X: Cheat Sheet"
date: 2015-02-21 00:41
comments: true
categories:
 - mac
 - osx
 - syslog
 - cheatsheet
---
This is a quick cheatsheet to work with [`syslog(1)`](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/syslog.1.html) implementation OS X uses.

`Console.app` provides a nice UI to access logs in mac, you can do some basic filtering and search, but its limited in terms of raw control a terminal gives you.

`/usr/bin/syslog` can be used to both send and receive logs. Alternatively [`logger(1)`](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/logger.1.html) can be used to send logs to syslog.

## Print logs from a specific facilitiy
```bash
# -w: similar to tailf
syslog -k Facility local1 -w
```

## Sending logs
```bash
# -l severity level
syslog -s "message"
```

## Sending logs upstream to another syslog server
Syslog can forward your logs too. The configuration resides in `/etc/syslog.conf`. You can append forwarding rules in this file, format is
```
# Tab separated
Facility.Level    @IPADDR:PORT
```
After this reload syslog daemon.
```
sudo launchctl unload /System/Library/LaunchDaemons/com.apple.syslogd.plist
sudo launchctl load /System/Library/LaunchDaemons/com.apple.syslogd.plistp
```

# Extra reading
1. [`asl.conf(5)`](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man5/asl.conf.5.html) - Configuration file for Apple Syslog Log (A syslog superset apple implements), this is where all the logic to route logs are set
facility.level
