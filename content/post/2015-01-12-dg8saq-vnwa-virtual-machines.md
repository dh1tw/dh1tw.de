---
title: 'DG8SAQ VNWA & Virtual Machines'
author: Tobias (DH1TW)
layout: post
date: 2015-01-11T22:46:15+00:00
url: /dg8saq-vnwa-virtual-machines
categories:
  - Hardware
tags:
  - Measurements
  - vnwa
thumbnailImage: "img/2015/01/vnwa.jpg"
thumbnailImagePosition: "left"

---
 A few years ago I migrated almost entirely to OSX & Ubuntu. However I still had to maintain a Windows copy on one of my harddrive partitions, since a few applications were just available for Windows. In particular, [DG8SAQ&#8217;s superb Vector Network Analyzer (VNWA)][1] software. I can already use most of the applications in a Virtual machine, with the benefit of not having to reboot and change the OS, but DG8SAQ&#8217;s software with it&#8217;s USB I/O always gave me hard time. Finally I figured out what need&#8217;s to be changed. Now the VNWA runs also smoothly in a Virtual Machine.

<!--more-->

# My virtual Machine

Since my main OS in Mac OSX (currently version 10.10) I&#8217;m using [Parallels Desktop][2]. It has the big advantage that the Guest OS (in this case Windows 8.1) can be either booted from it&#8217;s partition or used in a Virtual Machine within OSX. I also like Oracle&#8217;s free [VirtualBox][3] and will eventually migrate one day entirely to Virtualbox.

# Buffer is key

Whenever I tried to operate my VNWA within the Virtual Machine, the results where unusable. Despite that I&#8217;m using a decently equipped MacBook (Quad Core & 16 GByte Ram), I just couldn&#8217;t make it work. The final trick was the result of a discussion with my friend Hardy, [DL1GLH][4]. Since he&#8217;s using the same VNWA on a very old Laptop (600MHz Single Core), he had to **increase the Audio Buffer size**. And indeed, after increasing the Audio Buffer size from 3000 to 6000 samples, the VNWA works now also smoothly in my virtualized Windows 8.1 installation. It&#8217;s slightly slower, but almost not noticeable.

## How to increase the Audio Buffer length

Go to: _VNWA Software > Options > Audio Settings_. The screenshot below will help you to find the parameter.

{{< figure src="/img/2015/01/vnwa-audio-buffer-size.jpg" link="/img/2015/01/vnwa-audio-buffer-size.jpg" >}}

 [1]: http://http://www.sdr-kits.net
 [2]: http://www.parallels.com/de/products/desktop/
 [3]: https://www.virtualbox.org
 [4]: http://www.dl1glh.de