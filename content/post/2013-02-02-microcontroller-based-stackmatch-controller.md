---
title: Microcontroller based Stackmatch Controller
author: Tobias (DH1TW)
layout: post
date: 2013-02-02T13:48:17+00:00
url: /microcontroller-based-stackmatch-controller
categories:
  - Hardware
tags:
  - embedded software
  - hardware
  - Software tools
  - stackmatch
thumbnailImage: "img/2013/02/stackmatch_controller.jpg"
thumbnailImagePosition: "bottom"

---

At our Contest Station ED1R we have on each highband 3 Yagis available. In 2012 [I built 4 high power Stackmatches][1] in order to switch and combine them properly. Since I never liked the way of WX0B's stackmatch controllers with the rotative knob, a microcontroller and button based solution was the answer. After a few contests the solution has proven it's reliability and comfort.

<!--more-->

## The platform

My good friend Pablo, EA4TX suggested to reuse his ARS Interface box, instead of developing everything from scratch. A welcome offer! Pablo's ARS box, which is a USB powered, [enhanced replacement/addon control for any kind of rotator][2], brings everything I needed:

  * Microcontroller with USB Interface
  * 5 Relay based output ports
  * Available Input for Pins
  * LCD Display
  * 4 Buttons

{{< figure src="/img/2013/02/IMG_2183.jpg" link="/img/2013/02/IMG_2183.jpg" >}}

So all I had to do was "just" to write a new Software, adding two plugs and connecting my cables.

Here are the main features of the ED1R Stackmatch Controller:

- Names can be loaded for all antennas
- PTT Sensitive to select different RX and TX antennas
- Control through buttons or USB messages
- Ready for 4O3A Triplexor
- Comfortable Configuration through Windows application


{{< figure src="/img/2013/02/waessb2012_019.jpg" link="/img/2013/02/waessb2012_019.jpg" >}}

## Configuration Software

This little Windows program allows a comfortable configuration of the individual Stackmatches through the USB port.

{{< figure src="/img/2013/02/stack-control1.png" link="/img/2013/02/stack-control1.png" >}}

Pablo, EA4TX has already developed an TCP/IP based client/server which allows us to control the Stackmatches from any operator position. This is another great advantage. In a competitive M/S or M/2 environment all three Stations need access to the Antennas.

 [1]: https://www.dh1tw.de/new-stackmatches-for-ed1r
 [2]: http://www.ea4tx.com