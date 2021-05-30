---
title: Debugging the RS232 serial port
author: Tobias (DH1TW)
layout: post
date: 2008-11-21T11:00:27+00:00
url: /debugging-serial-port
categories:
  - Hardware
tags:
  - CW-Skimmer
  - FT1000MP
  - Modifications
  - N1MM
  - Realterm
  - VSPE
  - Win-Test
thumbnailImage: "img/2009/09/titelbild.jpg"
thumbnailImagePosition: "left"
---

In this article, we will investigate how various Contest programs (Win-Test, N1MM, and CW-Skimmer) communicate with the FT1000MP shortwave transceiver over the serial port. We will see what happens when multiple programs try to talk to the transceiver at the same time, what problems appear and how we can successfully monitor and debug them.

<!--more-->

# Introduction

A couple of weeks ago [I modified my Yaesu FT1000MP](https://www.dh1tw.de/bandscope-ft1000mp) short wave transceiver to be able to use it with an external software defined radio (SDR). For decoding morse code (CW), Alex Shovkoplyas, VE3NEA wrote the neat software [CW-Skimmer](http://www.dxatlas.com) which can decode up to 700 CW stations in conjunction with a wideband receiver.

In the "old days" the transceiver was connected exclusively to logging software like Win-Test or N1MM. With the introduction of CW-Skimmer, another application announced access to the transceivers interface. Unfortunately, Windows **allows** natively **only one application** to use the serial (com)-port **at any moment.**

{{< figure src="/img/2009/09/pc_config3.jpg" link="/img/2009/09/pc_config3.jpg" >}}

But nobody is wondering, that in the golden days of Computer Virtualization also virtual COM-Port drivers became available. Several companies offer a variety of virtual COM port/splitter/router applications. This is a list of the ones I found:

- [Eltima Virtual Ports](http://www.virtualserialport.com/)
- [KernelPro's Advanced Virtual Com Port](http://www.advancedvirtualcomport.com/index.html)
- [Fabulatech's Virtual Serial Port Kit](http://www.virtual-serial-port.com)
- [Eterlogic's VSPE](http://www.eterlogic.com)

**A Virtual Com-Port Splitter allows us to access the same physical Com-Port of a Computer multiple times simultaneously**. My favorite one is Eterlogic's VSPE. It's intuitive, very reliable, and freeware!

This is how the configuration looks like now:

{{< figure src="/img/2009/09/pc_config4.jpg" link="/img/2009/09/pc_config4.jpg" >}}

Now we have established the communication, we can start with the problems 😉

Virtual Serial Splitter allows us to use the same com port with several applications, however, they have no intelligence regarding packet routing. Let's have a closer look at what I mean with packet routing.

The virtual splitter sends the data requests from both applications to the transceiver:

{{< figure src="/img/2009/09/pc_config5.jpg" link="/img/2009/09/pc_config5.jpg" >}}

{{< figure src="/img/2009/09/pc_config61.jpg" link="/img/2009/09/pc_config61.jpg" >}}

In this case, Win-Test has some trouble. With a polling ratio of 1:10 (Win-Test: 100ms and CW-Skimmer: 1000ms) the frequencies are displayed in both applications correctly. Unfortunately **Win-Test**'s Bandmap always **toggles** between the first and second VFO wrongly **indicating "Split" Operation**. During serious operations, this gets quite soon very annoying especially during crossband operation, when QSOs are accidentally logged on the wrong band.

See the following two screenshots when the band map is in the "normal" and "split" operation.

{{< figure src="/img/2009/09/no_split.jpg" link="/img/2009/09/no_split.jpg" >}}

However, **N1MM** doesn't show this behavior at all. It **works smoothly** in conjunction with CW-Skimmer on the same COM Port. So, what is the difference? **Isn't serial communication = serial communication? No, it isn't!**

# FT1000MP Serial Communication Protocol

Before we go into deeper analysis, we need to know what we are looking for. Therefore we should take a brief look at the FT1000MP communication protocol. I picked out the most important messages. Please note that the transceiver's serial communication protocol is explained very well in the FT1000MP user manual (page 73 & 83). The manual can be downloaded from several websites.

For the FT1000MP we distinguish between "command (request) messages" and "answer messages".

**Command messages consist of 5 bytes** (using hex representation).


The two most **important commands** are:

{{< highlight text >}}

Request (HEX): 00 00 00 03 10 -> "Please send me MAIN VFO A & Sub VFO B Data"
(i.e. Frequency, Band data, filter settings, ...etc)

{{< /highlight >}}

{{< highlight text >}}

Request (HEX): 00 00 00 00 FA -> "Please send me the status flags"
(i.e. split operation, dual reception, Antenna tuning in progress, ...etc).

{{< /highlight >}}

{{< highlight text >}}

Reply on (HEX) 00 00 00 30 10:

{{< /highlight >}}

{{< figure src="/img/2009/09/answer_status.jpg" link="/img/2009/09/answer_status.jpg" >}}

{{< figure src="/img/2009/09/answer_frequency.jpg" link="/img/2009/09/answer_frequency.jpg" >}}

This is the description of status flag 1 (which is for our purpose the most important one, because it contains the "Split Mode" setting):

{{< figure src="/img/2009/09/status_flag1.jpg" link="/img/2009/09/status_flag1.jpg" >}}

# Tracing the serial interface

Now that we know what we have to expect we'll start tracing the serial interface.

For tracing, monitoring, and debugging purpose I recommend the following tools:

- Portmon part of Microsoft's Sysinternal Suite
- [Free Serial Port Monitor](http://www.serial-port-monitor.com)
- [Realterm](http://realterm.sourceforge.net/)

** Let's begin with the communication between N1MM and the FT1000MP:**

{{< figure src="/img/2009/09/n1mm_com.jpg" link="/img/2009/09/n1mm_com.jpg" >}}

{{< figure src="/img/2009/09/n1mm_trace.jpg" link="/img/2009/09/n1mm_trace.jpg" >}}

We can see that **N1MM** is requesting all data (**two** data requests) within a **single package**:

Request (HEX):

{{< highlight text >}}

00 00 00 03 10 00 00 00 00 FA

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

11 01 55 FA 40 FF D0 02 B3 00 11 B3 11 11 11 00 (VFO1)
11 01 56 5C 00 00 00 02 B3 00 11 B3 11 11 11 00 (VFO2)
0A 20 00 03 93                                  (Status Flags)

{{< /highlight >}}

** Let's try Win-Test and the FT1000MP:**

{{< figure src="/img/2009/09/wintest_com.jpg" link="/img/2009/09/wintest_com.jpg" >}}

{{< figure src="/img/2009/09/wintest_trace.jpg" link="/img/2009/09/wintest_trace.jpg" >}}

We can see that Win-Test is requesting the data in two consecutive packages:

Request (HEX):

{{< highlight text >}}

00 00 00 03 10

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

11 01 55 FA 40 FF D0 02 B3 00 11 B3 11 11 11 00 (VFO1)
11 01 56 5C 00 00 00 02 B3 00 11 B3 11 11 11 00 (VFO2)

{{< /highlight >}}

Request (HEX):

{{< highlight text >}}

00 00 00 00 FA

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

0A 20 00 03 93 (Status Flags)

{{< /highlight >}}


**And now we will trace the communication between CW-Skimmer and the FT1000MP:**

{{< figure src="/img/2009/09/cw-skimmer_com.jpg" link="/img/2009/09/cw-skimmer_com.jpg" >}}

{{< figure src="/img/2009/09/cwskimmer_trace.jpg" link="/img/2009/09/cwskimmer_trace.jpg" >}}

Well, and CW-Skimmer is, requesting quite a lot of additional information.

Request (HEX):

{{< highlight text >}}

00 00 00 02 10

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

11 01 55 FA 40 FF D0 02 B3 00 11 B3 11 11 11 00

{{< /highlight >}}

Request (HEX):

{{< highlight text >}}

00 00 00 03 10

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

11 01 55 FA 40 FF D0 02 B3 00 11 B3 11 11 11 00 (VFO1)
11 01 56 5C 00 00 00 02 B3 00 11 B3 11 11 11 00 (VFO2)

{{< /highlight >}}

Request (HEX):

{{< highlight text >}}

00 00 00 00 FA

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

0A 20 00 03 93 (Status Flags)

{{< /highlight >}}

Request (HEX):

{{< highlight text >}}

00 00 00 01 FA

{{< /highlight >}}

Answer (HEX):

{{< highlight text >}}

0A 20 00 00 09 00 (Status Flag)

{{< /highlight >}}

Okay, honestly CW-Skimmer doesn't need that much information. **CW-Skimmer only needs the frequency of the VFOs**. To reduce the possibility of message interferences on the com port it is advisable to **reduce the traffic** and length to the amount as little as necessary. Due to the fantastic flexible interface of [VE3NEA's Omnirig](http://www.dxatlas.com/OmniRig) (that's CW-Skimmers Transceiver Interface engine), I **changed the communication/request pattern** to "N1MM style".


# Multiple Software accessing a single COM Port

Well, so far we haven't seen any conflict. Let's analyze the serial port while **CW-Skimmer and Win-Test** are accessing it** simultaneously**. The configuration looks like this:

{{< figure src="/img/2009/09/cwskimmer_wintest_analysis.jpg" link="/img/2009/09/cwskimmer_wintest_analysis.jpg" >}}

{{< figure src="/img/2009/09/cwskimmer_wintest_trace.jpg" link="/img/2009/09/cwskimmer_wintest_trace.jpg" >}}

We can see that some of the messages are **mixed up** and other **produce junk**. In the case of the "status request" (00 00 00 00 FA) we can see that answers (or the bytes that win-test thinks to receives) alter in the first byte (remember the #1 Status byte). This would mean the one time the #1 status byte is set to HEX: 0x11 -> 1111 1111 and the other time to Hex: 0x0A -> 0000 1010. This would **toggle bit 0 "Split Mode" flag**.

Tracing the connection with **N1MM and CW-Skimmer (modified communication pattern)** shows better answers. At least there seem to be no more clashed packages. Please note that FT1000MP seems to respond by repeating twice the requested information. Luckily, both applications can handle this without any problem.

{{< figure src="/img/2009/09/cwskimmer_n1mm_trace.jpg" link="/img/2009/09/cwskimmer_n1mm_trace.jpg" >}}

# Verification

At this stage, we already have isolated the problem pretty well.

1. VFO Data and Status bytes should be requested in one "package"

2. If they are requested in two separated "packages" this can cause trouble and "misunderstanding".

3. The aborted messages and package clashes cause Win-Test to misinterpret the first status byte (which contains the &"Split-Mode" flag).

To finally verify these theses we will simulate the FT1000MP by replacing it with the HEX-capable Terminal Program Realterm.

As mentioned, we connected logically through a virtual Com-Port (VSPE "Pair") with our terminal program to the "other side", where the FT1000MP should be. In Realterm we can see that Win-Test is trying to poll the FT1000MP. We will now feed the answers we traced earlier to find out if our theses are correct:

{{< figure src="/img/2009/09/realterm_config.jpg" link="/img/2009/09/realterm_config.jpg" >}}

{{< figure src="/img/2009/09/realterm.jpg" link="/img/2009/09/realterm.jpg" >}}

First Win-Test Request (HEX):

{{< highlight text >}}

00 00 00 03 10

{{< /highlight >}}

First Realterm Answer (HEX):

{{< highlight text >}}

11 01 55 FA 40 FF D0 02 B3 00 11 B3 11 11 11 00
11 01 56 5C 00 00 00 02 B3 00 11 B3 11 11 11 00

{{< /highlight >}}

Second Win-Test Request (HEX):

{{< highlight text >}}

00 00 00 00 FA

{{< /highlight >}}

Second Realterm Answer (HEX):

{{< highlight text >}}

0A 20 00 03 93 (Status Flags)

{{< /highlight >}}

alternative second Realterm Answer (HEX):

{{< highlight text >}}

11 20 00 03 93 (Status Flags)

{{< /highlight >}}

And indeed, as soon as we feed the second message, Win-Test starts **toggling the VFOs**.

# Conclusion

We have seen how it is possible to analyze and investigate a problem. In detail, we have investigated the behavior of various programs with a non-standard configuration by allowing these programs to talk simultaneously over the same serial port with an HF transceiver. By using serial analyzing software we found out that there is indeed a difference in how to obtain the same data from the transceiver. In the end, we finally verified how an optimum data request should look in a virtual com port environment.

I'll contact now the producers of Win-Test and kindly ask them if it might be possible to change the pattern of the requesting command. Even better would be, if the Omni-Rig Engine would be directly supported by Win-Test.

During this investigation I used the following software versions:

- Windows XP: SP2 (Administrative rights)
- Win-Test: 3.21.0
- N1MM: 8.0.0
- CW-Skimmer: 1.2
- VSPE: 0.80.2.385
- Free Serial Port Monitor: 3.31
- Realterm: 2.0.0.57