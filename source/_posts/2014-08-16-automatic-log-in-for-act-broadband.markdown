---
layout: post
title: "Automatic log-in for ACT Broadband"
date: 2014-08-16 19:14
comments: true
categories: 
 - scripts
 - bangalore
 - ACT broadband
---

In my openion [ACT](http://portal.acttv.in) is the best ISP in [Bangalore](http://en.wikipedia.org/wiki/Bangalore), I found this network to be much better than any other provider in terms of reliability and the bandwidth, they seem very hacker friendly too, logging in as straightforward as a simple HTTP POST. 

I have this script running in my router so that I never have to bother logging in.

```bash
#!/bin/bash

USERNAME=""
PASSWORD=""

curl --data 'act_username=${USERNAME}&act_password=${PASSWORD}&login=login' \
  http://portal.acttv.in -o /dev/null
```


