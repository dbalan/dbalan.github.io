---
layout: post
title: "Debugging RTEMS with GDB"
date: 2013-06-23 19:40
comments: true
categories: 
 - RTEMS
 - GSoC
 - GDB
---

RTEMS is difficult to debug, since the default GDB behaviour follows a language based approch and developer will have to debug the application+RTEMS stack as a whole. We are in process of developing a new set of extenstions for GDB to play nice with RTEMS. The intial code is available in this [github repository](https://github.com/dbalan/rtems-gdb).

To use the extenstion, 
 - Clone the repository
{% codeblock lang:bash %}
git clone git@github.com:dbalan/rtems-gdb.git
{% endcodeblock %}
 - Assuming you have a working [RTEMS toolchain](/blog/2013/05/28/getting-started-with-rtems-on-archlinux/), spin up the GDB and source the code.
{% codeblock lang:bash %}
$ sparc-rtems4.11-gdb 

GNU gdb (GDB) 7.5.1
Copyright (C) 2012 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "--host=x86_64-linux-gnu --target=sparc-rtems4.11".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
(gdb) source path/to/clone/__init__.py 
RTEMS GDB Support loaded
(gdb) 
{% endcodeblock %}

Here is a sneak peak of what will be capable:
{% gist 5428535 %}
{% gist 5488653 %}

