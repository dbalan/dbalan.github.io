---
author: dhananjayishere
comments: true
date: 2011-10-11 03:33:00
layout: post
slug: ffmepg-nokia-7210-video-clips
title: FFmpeg + Nokia 7210 Video Clips.
wordpress_id: 74980538
categories: GNU/Linux Multimedia Tips
---

Nokia 7210 supports video clips of container mp4 with following specifications.

 Video Codec: mpeg4
Video Size: 320x240
Bit Rate: 500
Frame Rate: Auto
Aspect: Auto
Same Quality: False

 Audio:
Audio Codec: mpeg4aac
Bit Rate: 96
Sample Rate: 44100
Channels: 1 (Mono)
Disable Audio: False

 So to make a clip playable in phone,

 Use

 ** ffmpeg -i <infile> -b 500 -s 320x240 -f mp4 -acodec libfaac -vcodec mpeg4 <outfile>**
