---
title: 4O3A Triplexor
author: Tobias (DH1TW)
layout: post
date: 2013-03-14T23:34:52+00:00
url: /4o3a-triplexor
categories:
  - Hardware
tags:
  - antennas
  - ed1r
  - triplexor
featured: "triplexor.jpg"
thumbnailImage: "img/2013/03/triplexor.jpg"
thumbnailImagePosition: "bottom"
---

Until today, I'm fascinated by what can be achieved with good filters. At our Contest Station [ED1R][1] we bought a Triplexor (10m/15m/20m) to be able to use our new [Optibeam OB11-3][2] on the three bands simultaneously.

<!--more-->

## Motivation

At ED1R we only have one tall tower with 20m height. While we can finish in contests within the Top10 of our category, results showed that the high bands need to be boosted to get a permanent seat in the Top3 ranks. Since Vertical steel equity is restricted, we thought that a big Tribander on top of the tallest tower with a [4O3A Triplexor][3] would give us _the biggest bang for the buck_.

{{< figure src="/img/2013/03/4o3a-triplexor.png" link="/img/2013/03/4o3a-triplexor.png" >}}

After the successful installation of the Triplexor, each of the three high bands (10m / 15m / 20m) has now 3 Antennas available:

  1. Rotatable Monobander
  2. Monoband Yagi fixed towards USA or EU
  3. OB11-3, connected through the triplexor

## Schematic

The schematic below shows the setup:

{{< figure src="/img/2013/03/triplexer-at-so2r-with-switching.png"
link="/img/2013/03/triplexer-at-so2r-with-switching.png" >}}

A prerequisite for the Triplexor is a set of High Power Bandfilters. Achieving >100dB attenuation on a harmonic band is quite an engineering challenge. To ensure proper operation, the input terminals of the Triplexor have to be terminated at any time with 50Ohm. Therefore I built three switchable dummy loads.

{{< figure src="/img/2013/03/IMG_2156.jpg" link="/img/2013/03/IMG_2156.jpg" >}}

The picture above shows the Triplexor mounted on a timber panel with the three switchable dummy loads

{{< figure src="/img/2013/03/IMG_2152.jpg" link="/img/2013/03/IMG_2152.jpg" >}}

The switchable dummy load consists mainly of a [50Ohm/100W RF resistor][4], connected to a heatsink and a 16A/230V relais. If no power is applied, the input terminal from the Triplexor is always connected to the load. For wiring, a high-power Teflon cable has been used. An LED indicates the usage.

{{< figure src="/img/2013/03/ed1r_stackmatches.jpg" link="/img/2013/03/ed1r_stackmatches.jpg" >}}

This shows the new antenna switching system of ED1R. Four [homebrew Stackmatches][5], a 10x2 Antenna switch, the 4O3A High power Bandfilters, and the 4O3A triplexor.

{{< figure src="/img/2013/03/ed1r_antenna-switching.jpg" link="/img/2013/03/ed1r_antenna-switching.jpg" >}}

The same setup, just with all wires connected

{{< figure src="/img/2013/03/waessb2012_019.jpg" link="/img/2013/03/waessb2012_019.jpg" >}}

I updated and included the Dummy-Load switching into the software of our [Microcontroller based Stackmatch Controllers][6]. Now the relays inside the load will be triggered whenever the OB11-3 is selected.

## Triplexor in Action

After the successful installation, Javi, EC4DX recorded a short video to demonstrate the performance of the Triplexor. Unfortunately, we missed recording the harmonics on 10m while transmitting on 20m. But the video gives you anyhow a good idea about how smooth it works.

## Conclusion

I invested in design, hardware, and software for roughly 40 hours during various evenings and weekends. Ranko's Triplexor is a truly great invention. Except for a small portion (+-20kHz) of the 20m's harmonic on 10m, almost no interference can be noted. It's almost a bit spooky to send 1,5kW on 10m and 15m through a coax cable while listening on 20m with the same antenna.

 [1]: http://www.ed1r.com
 [2]: http://www.optibeam.info/index.php?article_id=111&clang=1
 [3]: http://www.4o3a.com/index.php?option=com_content&view=category&layout=blog&id=127&Itemid=509
 [4]: http://www.box73.de/product_info.php?products_id=1583
 [5]: https://www.dh1tw.de/new-stackmatches-for-ed1r
 [6]: https://www.dh1tw.de/microcontroller-based-stackmatch-controller