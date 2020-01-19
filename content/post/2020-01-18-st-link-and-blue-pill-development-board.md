---
title: "ST-Link & Blue Pill Development board"
author: Tobias (DH1TW)
date: 2020-01-18T21:00:00+01:00
layout: post
categories:
  - Embedded
  - STM32
tags:
  - stm32
  - microcontroller
  - st-link
  - aliexpress
thumbnailImage: "img/2020/01/stlink-teaser.jpeg"
thumbnailImagePosition: "bottom"
---

The [ST-Link/v2](https://www.st.com/en/development-tools/st-link-v2.html) is an in-circuit debugger and programmer for the STM32 and STM8 micro controller families. Due to it's capabilities, it is an extremely popular device and clones are available from your preferred chinese trading platform for less than 5 Euro. I recently ordered a few of these cheap ST-Link/v2 clones for a new project. However making them work was pretty frustrating. Read on to learn about the problem, the symptoms and the (super) **easy fix**.

<!--more-->

## Connecting the 'Blue Pill'

Over the years I've used occasionally the '[Blue Pill](https://stm32-base.org/boards/STM32F103C8T6-Blue-Pill)' which is a little development board, comparable in size with the better known [Arduino Nano](https://store.arduino.cc/arduino-nano), but with a modern and more capable ARM Cortex M3 CPU ([STM32F103C8T6](https://www.st.com/en/microcontrollers-microprocessors/stm32f103c8.html)).

{{< figure src="/img/2020/01/stlink-with-bluepill-small.jpeg"
    link="/img/2020/01/stlink-with-bluepill.jpeg"
    caption="Figure 1: ST-Link/v2 knock-off connected to a 'Blue Pill' development board" >}}

In the past I used an original [ST-Link/V2](https://www.st.com/en/development-tools/st-link-v2.html), but it became a victim of my last move. I couldn't find it anymore. So I ordered a few clones on Aliexpress along with a bunch of 'Blue Pill' boards. The boards are certainly also knock-offs, although the CPU appears to be genuine.

## Software tooling

I'm a big fan of Microsoft's free and cross-platform Editor/IDE [Visual Studio Code](https://code.visualstudio.com/), but when it comes to ST micro controllers I prefer to use their [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html). ST has come a long way integrating their stuff into [Eclipse](https://www.eclipse.org/), but in 2020 it's now working well, even on MacOS :sweat_smile:.

ST provides also some optional software tools for their micro controllers. In particular I found the [STM32 ST-Link Utility (STSW-LINK004)](https://www.st.com/en/development-tools/stsw-link004.html) to be quite helpful - although it's only available for Windows.

{{< figure src="/img/2020/01/stm32-stlink-utility-small.jpeg"
    link="/img/2020/01/stm32-stlink-utility.jpeg"
    caption="Figure 2: Screenshot of the STM32 ST-Link Utility" >}}

## The problem

The ST-Link/v2 has a 10 pin interface through which it interfaces with the development board. The pin-out diagram is printed on top of the ST-Link/v2. After connecting the two devices, I tried to upload a simple test program, but it just wouldn't work and the error messages were also rather cryptic.

## The symptoms

Despite that the ST-Link/v2 was properly recognized, I wasn't able to connect or upload anything to the development board.
Poking around with the ST-Link/v2 settings I was confronted with the following error messages over time:

``` text
- "Error in initializing ST-LINK device. Reason: No device found on target"
- "Can not connect to target! Please select "Connect Under Reset" mode from Target->Settings menu and try again. If you're trying to connect to a low frequency application , please select a lower SWD Frequency mode from Target->Settings menu"
- "If the target is in low power mode, please enable "Debug in Low Power mode" option from Target->settings menu"
- "No device found on target"
- "No STM32 target found"
```

In order to ensure that this wasn't a hardware issue, I tried of course several combinations of ST-Link/v2s and development boards. Unfortunately, none of them worked.

## Success

Since none of my 'Blue Pill' development boards were recognized by none of the ST-Link/v2 programmers, I suspected a rather systematic error. Needless to say that I tried to google the error messages above, but none of the shown links were conclusive.

After some further digging through the box in which I store my micro controller stuff, I found to my own surprise another ST-Link/v2 knockoff which I must have purchased some years ago (and since forgotten about it - hi).

{{< figure src="/img/2020/01/stlink-black-blue-small.jpeg"
    link="/img/2020/01/stlink-black-blue.jpeg"
    caption="Figure 3: Two ST-Link/v2 knockoffs" >}}

After swapping the blue ST-Link for the black one, I was suddenly able to connect to the 'Blue Pill' development board!

 {{< giphy 4xpB3eE00FfBm >}}

## The solution

With a working setup, I investigated why the blue ST-Links didn't work. The most obvious difference is the pin out diagrams printed on the respective ST-Link knock-off. Opening the blue ST-Link revealed the following:

{{< figure src="/img/2020/01/stlink-pcb-bottom-small.jpeg"
    link="/img/2020/01/stlink-pcb-bottom-small.jpeg"
    caption="Figure 5: ST-Link/v2 PCB bottom side" >}}

**The pin names on the PCB differ from the diagram printed on the ST-Link/v2 enclosure!!!**

{{< giphy l1OnUrNlAjI1gqmqNE >}}

After re-wiring, the blue ST-Link/v2 also worked as expected.

For the sake of completeness, here **the correct pin-out**:

Pin  | Row    | Name
-----|--------|--------
1    | Upper  | RST
3    | Upper  | SWIM
5    | Upper  | GND
7    | Upper  | 3.3V
9    | Upper  | 5.0V
2    | Bottom | SWCLK
4    | Bottom | SWDIO
6    | Bottom | GND
8    | Bottom | 3.3V
10   | Bottom | 5.0V

## Bottom line

Out of curiosity I checked Amazon, Ebay and a few of the chinese trading platforms and to my surprise almost all of the ST-Link/v2s shown have the wrong pin-out diagram printed on the enclosure. I hope that the manufactures will correct the diagram in the future. In the meanwhile I hope this article was helpful and saved you from falling into the same trap :stuck_out_tongue_winking_eye:.
