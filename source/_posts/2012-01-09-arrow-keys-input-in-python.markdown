---
author: dhananjayishere
comments: true
date: 2012-01-09 14:30:00
layout: post
slug: arrow-keys-input-in-python
title: Arrow Keys input in python.
wordpress_id: 93005403
categories:
- Programing
- Python
---

I had an assignment to write an applicaion to control a toy helicopter. It should accept the inputs from the arrow keys and then generate a serial signal. The serial port is connected to the interfacing circutary.

The major problem I faced was how to take arrow keys as input? Using the technical jargon - implement a non-bufferd input. A code to do it in console can be found [here](http://code.activestate.com/recipes/134892-getch-like-unbuffered-character-reading-from-stdin/). But its dirty and is implemented in a complex way that usage is little bit diffcult. At console level the code becomes more os-specific, as you can see from the above code. It has diffrent defenitions to implement the feature in each os.

The easy way to do this is using any windowing tool kits around, they all have a key logging abstraction implemented. Like this [code](http://stackoverflow.com/a/4205490). it uses the tkinter toolkit to read input. The way I suggest is using pygame, because it is designed to this stuff. (Which game doesnt have a single use arrow key used?)

You can get the keys from

> pressed_keys = pygame.key.get_pressed()

and the key name as

>
>
>     for key_constant in pressed_keys:  key_name = pygame.key.name(key_constant)


Then its just a matter of comparing them with the key name,( of arrow keys in our case).

> if key_constant == 'up':
>
> port.write(_up_data)


The complete code is available at, [https://github.com/dhananjaynav/Scripts/blob/master/castalia/helicontrol.py](https://github.com/dhananjaynav/Scripts/blob/master/castalia/helicontrol.py)
