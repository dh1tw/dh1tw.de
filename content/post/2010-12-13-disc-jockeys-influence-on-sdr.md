---
title: Disc Jockeys influence on SDR
author: Tobias (DH1TW)
layout: post
date: 2010-12-12T22:14:41+00:00
url: /disc-jockeys-influence-on-sdr
categories:
  - Software Defined Radio
tags:
  - DJ Console
  - Softrock
  - Software Defined Radio
  - Visual Studio 2008
thumbnailImage: "img/2010/12/powersdr-ui.jpg"
thumbnailImagePosition: "left"
---
The User Interface of computers suck when it comes to Radio Controlling. In January 2010 I got so annoyed by being forced to control the radio with keyboard and mouse that I finally decided to look for something else. Now, almost one year later I’m happy that I can present you an interesting alternative. The interface costs less than 100 USD, is commercially available and improves the overall SDR experience significantly.
<!--more-->

## The idea

While strolling through the shelves of the local consumer electronics retailer, I noticed some kids producing horrible noises by scratching on a digital turntable. When they left after a few minutes I went over to have a look by myself on this device. The device of suspect turned out to be a Disc Jockey Console which delivers an extensive set of functionality for ambitious DJs. Where Disc Jockeys used Vinyl a few decades ago, they have been replaced by MP3s, Digital Signal Processors and powerful PCs. However one thing has not changed – the **User Interface**.


Even if the turntables, the knobs and the buttons on such a console are directly converted into digital signals, the tactile feel is almost the same as on a record player from the seventies. For the DJ’s profession, keyboard and mouse are inadmissible. **Why change things proved systems which have been optimized over several decades just because the application is transferred from the analog into the digital domain?**

Exactly this question also applies to Software Defined Radio. I already [discussed the importance of the User Interface](https://www.dh1tw.de/does-sdr-really-suck) in another blog post – therefore I’ll come back now to the DJ Console 😉.

When I had the DJ Console in my fingers I realized that such a device would satisfy most needs for controlling a radio. It comes with two big turn wheels, more than twenty buttons and almost ten knobs.

{{< figure src="/img/2010/12/djconsole.jpg" link="/img/2010/12/djconsole.jpg" >}}

With this thought, the idea of a new SDR User Interface was born.

## The result

So, I just needed to connect the DJ Console to my PC and somehow use it to control an SDR software. Sounds easy, doesn’t it? Unfortunately it was not that easy. Now looking back on this project, it took me more than 100 hours, a couple of failures and a few drawbacks. I’ll share my experiences in another blog post. Now I’ll focus more on the result.

From the beginning it was very clear, that I do not want to develop my own SDR Software but instead, making **maximum reuse** of existing [building blocks, namely the RF and Signal processing building blocks](https://www.dh1tw.de/understanding-the-sdr-concept). Since I couldn’t find an SDR framework or software with proper Interfaces I had to look for an SDR software to modify and adapt to my needs.

I selected Flexradios PowerSDR as the Signal Processing building block because the sourcecode is published under the GPL license and the software itself made a stable impression. My good old Softrock clone added the RF part. The main focus of my work was the integration of the DJ Console into PowerSDR. While I had not only to add but also modify the PowerSDR source code, I’m quite happy with the result. Now let's have a detailed look on it!

{{< figure src="/img/2010/12/powersdr.jpg" link="/img/2010/12/powersdr.jpg" >}}

Within PowerSDR I can now select in “Setup” a new Tab called “UI Controller”. Here a connected Hercules DJ Console can be selected and individually configured.

{{< figure src="/img/2010/12/powersdr_setup.jpg" link="/img/2010/12/powersdr_setup.jpg" >}}

The sweetness of software is its configurability. I wrote a configuration mask which allows everyone to map the software’s function to a specific knob, button or wheel according to the operators’ individual preferences.

{{< figure src="/img/2010/12/powersdr_DJConsoleConfiguration.jpg"
  link="/img/2010/12/powersdr_DJConsoleConfiguration.jpg" >}}

The available functions have been divided into three groups:

- Buttons (On – Off)
- Turning Knobs (Value range 0…100)
- Turning Wheels (increment / decrement)

Currently the buttons of a Hercules DJ Console can be mapped to the following functions:

{{< figure src="/img/2010/12/djconsole_buttons.jpg" link="/img/2010/12/djconsole_buttons.jpg" >}}

- Lock VFO
- MultiRx On/Off
- Narrower Filter
- Wider Filter
- Next Mode
- Previous Mode
- Noiseblanker 1 On/Off
- Noiseblanker 2 On/Off
- RIT On/Off
- XIT On/Off
- Increase Tuning Steps
- Decrease Tuning Steps
- VFOA to VFOB
- VFOB to VFOA

Regarding the turning knobs, the following mapping is currently supported:

{{< figure src="/img/2010/12/djconsole_knobs.jpg" link="/img/2010/12/djconsole_knobs.jpg" >}}

- AF Gain (Overall Audio Volume)
- Ratio MainRx/SubRx
- RIT
- XIT
- Volume Rx1
- Volume Rx2

An finally the turning wheels can be used as

{{< figure src="/img/2010/12/djconsole_wheels.jpg" link="/img/2010/12/djconsole_wheels.jpg" >}}

- Frequency Control VfoA
- Frequency Control VfoB
- Controlling Filter Bandwidth

The following video will give you an overview how this works in practice:

{{< youtube NR-ZwUaffI8 >}}

Ensure that you watch this video in 720px Full HD! Sound is turned on after the first minute!

# So, what's next?

I would currently label the status of my add-on to PowerSDR “prototype”. Even if it works quite well for me, it has not been released to the public yet. My further effort on this will depend on the feedback from you.

Over the last month I was talking and complaining a lot about the bad User Interfaces for Software Defined Radios. The intention of this DJ Console integration was to prove that it is possible to have a decent UI for little money. Please recognize the importance of the User Interface building block. It is as important as the RF and Signal Processing building block. Please spread the word!

{{< figure src="/img/2010/12/IMGP5758-1.jpg" link="/img/2010/12/IMGP5758-1.jpg" >}}

If you like this project, **please leave me a comment** with **your thoughts**!

## **[update 13/12/2010]**

I received a couple of comments that this particular Hercules DJ Console MK2 is not sold anymore. This is true. However you might still find it for reasonable prices on ebay from time to time. On the other hand, Hercules has brought out a couple of new models.