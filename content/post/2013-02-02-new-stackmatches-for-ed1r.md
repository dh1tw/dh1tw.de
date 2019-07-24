---
title: New Stackmatches for ED1R
author: Tobias (DH1TW)
layout: post
date: 2013-02-02T13:04:31+00:00
url: /new-stackmatches-for-ed1r
categories:
  - Hardware
tags:
  - hardware
  - Measurements
  - stackmatch
thumbnailImage: "img/2013/02/stackmatch.jpg"
thumbnailImagePosition: "bottom"

---

One of last years projects was the improvement of our Contest Station ED1R. For the various Yagis we needed smart ways to combine antennas. Instead of buying commercial stackmatches (antenna combiners) I decided to build them up buy myself and adjust them to our needs.

<!--more-->

## HF part

A great resource is Mike's, [SM2WMV (SJ2W) website][1]. Mike is a professional RF engineer and he designed beautiful Stackmatch PCB's which he also makes available for purchase. Instead of spending hours in designing my own stackmatch PCB, I preferred to buy Mike's PCBs - especially at this price, a no-brainer.

{{< figure src="/img/2013/02/IMG_2176.jpg" link="/img/2013/02/IMG_2176.jpg" >}}

Basically all I had to do is purchasing the missing components, drilling the holes in the box and installing everything. I used two stacked FT240-61 ferrit cores for the transformers. All the transformers consist of 4 (10m & 15m) or 5 (20m & 40m) trifilar windings of 2mm enameled copper wire. Since impedance is very low (17 &#8211; 50 Ohm), no high voltages are expected. That&#8217;s why no additional (e.g. Telfon) insulated wires are necessary.

{{< figure src="/img/2013/02/IMG_2179.jpg" link="/img/2013/02/IMG_2179.jpg" >}}

In order to fix the Balun properly on the PCB I purchased from Hans, DK3YD high temperature resistant Delin washers.

{{< figure src="/img/2013/02/IMG_2177.jpg" link="/img/2013/02/IMG_2177.jpg" >}}

Above you can see the aluminium box I bought at the local electronic store. The PCB fits perfectly into the box.

{{< figure src="/img/2013/02/IMG_2182.jpg" link="/img/2013/02/IMG_2182.jpg" >}}

and for outside.

{{< figure src="/img/2013/02/IMG_2181.jpg" link="/img/2013/02/IMG_2181.jpg" >}}

This is how the stackmatch looks assembled

## Measurements

{{< figure src="/img/2013/02/S11-Measurements-with-50-Ohms-terminated-all-ports.png"
  link="/img/2013/02/S11-Measurements-with-50-Ohms-terminated-all-ports.png" >}}

S11 between the Input and the Output Ports is always better than -20dB (click to enlarge)

{{< figure src="/img/2013/02/S21-Port-Isolation-Antenna1.png"
  link="/img/2013/02/S21-Port-Isolation-Antenna1.png" >}}

Isolation between the ports is between -60dB (7MHz) and -40dB (28MHz) (click to enlarge)

{{< figure src="/img/2013/02/S21-Antenna2-with-Antenna1.png"
  link="/img/2013/02/S21-Antenna2-with-Antenna1.png" >}}

S11 and S21 of two antennas combined (3dB Splitting) (click to enlarge)

{{< figure src="/img/2013/02/S21-Antenna-3-worst-case.png"
  link="/img/2013/02/S21-Antenna-3-worst-case.png" >}}

S11 and S21 of three antennas combined (6dB Splitting) (click to enlarge)

## Stackmatches installed

{{< figure src="/img/2013/02/shack1.jpg" link="/img/2013/02/shack1.jpg" >}}

And finally all the stackmatches installed at ED1R above the 8-Pack and the 4O3A High Power Bandpass filters

[1]: http://www.sj2w.se/