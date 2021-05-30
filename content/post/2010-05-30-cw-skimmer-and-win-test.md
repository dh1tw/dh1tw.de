---
title: 'CW Skimmer, Win-Test & FT1000MP: my wish!'
author: Tobias (DH1TW)
layout: post
date: 2010-05-30T02:30:19+00:00
url: /cw-skimmer-and-win-test
categories:
  - Software Defined Radio
tags:
  - Bandscope
  - CW-Skimmer
  - FT1000MP
  - Win-Test
thumbnailImage: "img/2010/05/fingers_crossed.jpg"
thumbnailImagePosition: "left"

---
Three years ago I added a Software Defined Radio (Softrock Clone) to the 455kHz intermediate frequency of my FT1000MP shortwave receiver. The idea was to use it as a spectrum scope in conjunction with CW Skimmer. Unfortunately, the solution has one big disadvantage: I can't use it with Win-Test my favorite Contest Software. In a detailed investigation, I found out why CW Skimmer and Win-Test can not be used simultaneously with the same Radio. Now, about past 30 months later, the situation has improved. However, there is still one little change necessary to finally be able to use CW Skimmer and Win-Test with (my) FT1000MP. Read in this article what has changed and what is still missing (my wish)!
<!--more-->

## A short Recap

As mentioned in the teaser, I added a Software Defined Radio based [Spectrum Scope to my FT1000MP](https://www.dh1tw.de/bandscope-modification-yaesu-ft1000mp). Due to technical and operational reasons, I installed the Bandscope in the second receiver. The main advantages are that the second receiver provides a larger spectrum (20kHz) and is only used/changed occasionally since all QSOs are made with the Main receiver. This low-cost (< 20 USD), single band SDR kit (Softrock clone) in the IF, transforms my FT1000MP in a deluxe All-Band-Full-feature Software-Defined-Radio Hybrid.

Being a contest enthusiast I'm always trying to apply technologies to create a benefit in the contest (within the legal boundaries - of course). Unfortunately CW Skimmer and Win-Test (have been) using a different style in communicating with the FT1000MP. This made it impossible to use this setup in an operational contest environment. Check out my [Win-Test & CW Skimmer investigation](https://www.dh1tw.de/debugging-serial-port) if you like to go down as deep as bit & bytes level.

## What has improved?

Part of my resumé and suggestions of this investigation was, that it would be great if Win-Test would make use of the Omni-Rig engine which is used by CW-Skimmer. [Omni-Rig](http://www.dxatlas.com/omnirig) is a flexible software that manages the communication between one transceiver and several applications. With version 4.4 Oliver, F5MZN the author of Win-Test implemented the Omni-Rig engine! The following two images show the setup. In case you use an SDR band scope attached to the first receiver you might stop reading here - your problem is solved 😉

{{< figure src="/img/2010/05/cw-skimmer-and-win-test-general-setup.jpg"
  link="/img/2010/05/cw-skimmer-and-win-test-general-setup.jpg" >}}

_The image above shows the general setup including the software and hardware._

{{< figure src="/img/2010/05/win-test-with-omni-rig.jpg"
  link="/img/2010/05/win-test-with-omni-rig.jpg" >}}

This image shows how the VFO-A and VFO-B data are used by Win-Test and CW Skimmer. There are no more problems with Win-Test. Win-Test retrieves as expected the VFO-A frequency from VFO-A (provided by Omni-Rig) and VFO-B frequency from VFO-B (provided by Omni-Rig).

## The remaining problem

CW-Skimmer is currently retrieving the frequency information from VFO-A (first receiver). In case you have the SDR band scope (like I have) installed in the second receiver (VFO-B) you have a mismatch of frequency data. This means that CW Skimmer changes the frequency, whenever the VFO wheel of the Main receiver (VFO-A) is touched. However, this is not desired since the receiver which is connected to CW Skimmer is located in the second receiver and therefore logically connected to VFO-B.

## A possible solution

The following image shows how a possible solution could look like. When CW-Skimmer would provide an option to select the frequency source (VFO-A or VFO-B) the problem would be solved.

{{< figure src="/img/2010/05/cw-skimmer-switch-omni-rig.jpg"
  link="/img/2010/05/cw-skimmer-switch-omni-rig.jpg" >}}

Please note that changing the Omni-Rig Transceiver definition (e.g. flipping VFO-A/VFO-B) does not help in this case.

# My wish

Please, Alex - I would highly appreciate it if you could implement a frequency source (VFO-A or VFO-B) selection in the next version of CW Skimmer! In case you need any kind of assistance (e.g. testing) or further discussions, count on me!