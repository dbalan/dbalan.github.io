---
layout: post
title: "Getting started with RTEMS on Archlinux"
date: 2013-05-28 21:24
comments: true
categories:
- RTEMS
- GSoC
- Archlinux
---

The default RTEMS geting started does not cover the toolchain setup as it should be. It either redirects the user to download a ~1 GB distro or some pretty old RPMs. This shouldn't be like this.

There is an excellent tool called ***rtems source builder*** which can help a newbie setup RTEMS environment in a brisk. This post is the authors journal about how he did it, shared beacuse it might be beneficial to people looking to bootstrap RTEMS.

RTEMS is a real time operating system. It works on various type of hardware, and a devlopment setup is specific to the hardware of developers choice. Here I will demonstrate setting up a sparc toolchain with b-sis simulator.

### Setting up toolchain
First step of our RTEMS journey. A toolchain consists of a compiler, linker, debuggger and a simulator for the hardware. We need these tools to compile the RTEMS code and execute our programs.

This was a painful step in past. Cross compiler environments are nasty to get right. But dont worry, we have our wonderful rtems-source-builder to rescue.

rtems-source-builder automates the task of setting up this toolchain - it downloads the source files, builds them and installs in the system. It also have the option to make a tarball.

The actuall steps are documented here - [rtems-source-builder documentation][1], but if you prefer a capsule

- Setup directories and get source
```
$ cd
$ mkdir -p development/rtems/src
$ cd development/rtems/src
$ git clone git://git.rtems.org/chrisj/rtems-source-builder.git
$ cd rtems-source-builder
```
- Check environment.
```
$ ./source-builder/sb-check
RTEMS Source Builder environment is ok
```

- Build a sparc target
```
$ cd rtems
$ ../source-builder/sb-set-builder --log=l-sparc.txt /
--prefix=$HOME/development/rtems/4.11 4.11/rtems-sparc
```
this will produce binaries in `$HOME/development/rtems/4.11` directory.

__Note__: Default version of makeinfo in archlinux is incomaptible with tools we build, source-builder documentations says

>Archlinux, by default installs texinfo-5 which is incompatible for building GCC 4.7 tree. You will have to obtain texinfo-legacy from AUR and provide a manual override.

```
# pacman -R texinfo
$ yaourt -S texinfo-legacy
# ln -s /usr/bin/makeinfo-4.13a /usr/bin/makeinfo
```

### Building RTEMS
- First obtain the RTEMS code from github.
```
$ cd
$ mkdir -p development/rtems/repo
$ cd development/rtems/repo
$ git clone git@github.com:RTEMS/rtems.git
$ cd rtems
```

- Bootstrap the rtems and build code.
```
$ export PATH=/home/dhananjay/build/rtems/4.11/bin:$PATH
$ ./bootstrap
```

- Build a b-sis simulator code.
```
$ cd ..
$ mkdir b-sis && cd b-sis
$ ../rtems/configure --target=sparc-rtems4.11 --enable-rtemsbsp=sis --enable-tests=samples --enable-posix --prefix=/home/dhananjay/build/rtems/src/
$ make
```

### Running example code.
- Find the sample applications and execute them.

```
$ cd sparc-rtems4.11/c/sis/testsuites/samples/hello
$ ls

hello.exe  hello.num  hello.ralf  init.o  Makefile
$ sparc-rtems4.11-run hello.exe

*** GSOC HELLO WORLD TEST ***
Hello RTEMS World
Dhananjay Balan
*** END OF HELLO WORLD TEST ***
```

[1]: http://www.rtems.org/ftp/pub/rtems/people/chrisj/source-builder/source-builder.html "rtems-source-builder documentation"
