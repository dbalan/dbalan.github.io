---
author: dhananjayishere
comments: true
date: 2012-12-12 10:51:00
layout: post
slug: name-your-servers
title: Name your servers.
wordpress_id: 171537089
categories:
- Terminal
- SSH
- GNU/Linux
- Hack
---

If your day involves ssh-ing into various servers, you know how
cumbersome is to type all that details again and again. When the number
becomes large, you tend to confuse between host names, IPs and
usernames.

But, ssh allows you to alias them into cute nicknames you prefer.

The configuration file needed to be edited is  ``` ~/.ssh/config. ```

The sample configuration that should be append to this file for adding
alias _server_ to `user@example.org` is :

```
Host server
Hostname example.org
User user
```

Now all you have to do is
```
$ ssh server
```
