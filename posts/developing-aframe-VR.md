---
title: Developing WebVR using A-frame
date: 2021-12-21
slug: A-frame is a Javascript WebVR framework. Read how I've set up a development environment to create VR experiences
tags:
  - WebVR
  - VR
coverImage: /images/vr1280.jpg
author: Hadrian Cawthorne
authorImage: /images/hadrian.jpg
---
[A-Frame](https://aframe.io/) is a web framework for building 3D/AR/VR experiences. In this post, I'll explain how I use it, walk through the development environment that I use and offer some alternatives to that.

There are a few tools that you'll need:

- **A code editor**. I use [Atom](https://atom.io).
- **Access to Terminal**. I use [Ubuntu for Windows 10](https://ubuntu.com/tutorials/ubuntu-on-windows#1-overview), but you can use [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) or built-in Termainal on MacOS.

And that's it, really! The rest is done in either the code you write or by installing packages with Terminal*.

## *So what is Terminal?
It's a command-line interface that allows you to do stuff on your computer without using your graphical interface. I like to think of it as "pure" computing (or old-fashioned computing!).

You can see Windows Terminal below. It looks a bit like MS DOS, but it isn't!

![Screenshot of terminal in Windows](/images/terminal.png)

If you look at the commands I've written in Terminal above, I've **changed directory** (cd) to my Desktop, then I've **made a new folder/directory** (mkdir)  called *webvr_demo*. This saved me from having to use the mouse, right clicking etc. Just think of the effort saved there :laughing:
