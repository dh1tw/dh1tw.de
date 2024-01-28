---
title: "VNA Prototyping Board"
author: Tobias (DH1TW)
date: 2024-01-28T12:00:00+02:00
layout: post
categories:
  - Hardware
  - Measurements
tags:
  - vnwa
  - vna
  - sdr-kits
thumbnailImage: "img/2024/01/vna_testboard_teaser.jpg"
thumbnailImagePosition: "bottom"
---

Some years ago, [SDR-Kits](https://www.sdr-kits.net/) used to sell a small prototyping PCB perfect for experimenting with a Vector Network Analyzer. After many experiments, the female pin headers on my prototyping board wore out. Since SDR-Kits no longer sells it, I designed my version of this PCB. The KiCad sources of the [VNA prototyping/test board](https://github.com/dh1tw/vna-testboard) are available on my [Github profile](https://github.com/dh1tw/vna-testboard).

<!--more-->

## Design considerations

I designed the PCB with [KiCad](https://www.kicad.org/) version 7. Most likely, you have to change the footprint of the female SMA connectors on the PCB, since I used non-standard ones I had available at that moment. I designed the traces as microstrip lines, matching 50 Ohm. This resulting trace width is 1.85mm using **1,0mm PCB thickness** and an Epsilon r = 4.5 of the FR4 material. I get accurate results up to a few hundred Megahertz. The pin sockets have a 2.54mm spacing. I use Nylon M3 screws & nuts as feet. 

You can create a calibration kit with male pin headers and a 1% 50Ohm SMD resistor.

## License

I published the Design under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/deed.en).

## More pictures

{{< figure src="/img/2024/01/vna_testboard.jpeg"
    link="/img/2024/01/vna_testboard.jpeg"
    caption="The VNA Testboard">}}

{{< figure src="/img/2024/01/vna_testboard_with_original.jpeg"
    link="/img/2024/01/vna_testboard_with_original.jpeg"
    caption="The VNA Testboard with the original one from SDR-Kits">}}

{{< figure src="/img/2024/01/vna_testboard_pcb_layout.png"
    link="/img/2024/01/vna_testboard_pcb_layout.png"
    caption="The PCB Layout of the VNA testboard">}}
