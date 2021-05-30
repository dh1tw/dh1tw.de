---
title: Measuring ICE Bandpass Filter
author: Tobias (DH1TW)
layout: post
date: 2008-09-05T14:00:18+00:00
url: /ice-filter
categories:
  - Hardware
tags:
  - Bandpass Filter
  - Filter
  - ICE
  - Measurements
  - TAPR VNA
thumbnailImage: "img/2009/09/title.jpg"
thumbnailImagePosition: "left"
---

Today, I could measure the performance of the well-known ICE bandpass filters. Read more about the measurement results.
<!--more-->

# Introduction

A set of bandpass filters are necessary for a multi-signal environment. Almost all contesters have already experienced the problems of signal distortion in a multi-transmitter environment. Luckily bandpass filters help us to reduce the interferences between various transmitters.

Today there are bandpass filters available from:

- [Industrial Communication Enigneers (ICE)](http://www.iceradioproducts.com/filtersrf.html)
- [Dunestar](http://www.dunestar.com/)
- [Array solutions](http://www.arraysolutions.com)
- [4O3A](http://www.4o3a.com)
- [Wolfgang Wippmann (DG0SA)](http://www.wolfgang-wippermann.de)

A good construction manual of a 6 / 9 band filter set can be found on the website of the [Bavarian Contest Club](http://www.bavarian-contest-club.de) [DL2NBU / DL6RAI Bandpass filters (W3NQN Design)](http://www.bavarian-contest-club.de/projects/bandpassfilter/100W-BP.pdf)

# Measurement setup

As usual, I used my "poor man's" Vector Network Analyzer (VNA) from TAPR / Tentec.

In all diagrams <strong><span style="color: #ff0000;">S21 (forward transmission)</span></strong> and <span style="color: #008000;"><strong>S11 (reflexion / impedeance matching)</strong></span> were measured. The schematic and the picture below show the measurement setup.

{{< figure src="/img/2009/09/schematic.jpg" link="/img/2009/09/schematic.jpg" >}}

{{< figure src="/img/2009/09/messaufbau1.jpg" link="/img/2009/09/messaufbau1.jpg" >}}

## Measured band: 160m (1,8 MHz)

{{< figure src="/img/2009/09/160m.jpg" link="/img/2009/09/160m.jpg" >}}

## Measured band: 80m (3,5 MHz)

{{< figure src="/img/2009/09/80m.jpg" link="/img/2009/09/80m.jpg" >}}

## Measured band: 40m (7,0 MHz)

{{< figure src="/img/2009/09/80m.jpg" link="/img/2009/09/40m.jpg" >}}

## Measured band: 20m (14,0 MHz)

{{< figure src="/img/2009/09/20m.jpg" link="/img/2009/09/20m.jpg" >}}

## Measured band: 15m (21,0 MHz)

{{< figure src="/img/2009/09/15m.jpg" link="/img/2009/09/15m.jpg" >}}

## Measured band: 10m (28,0 MHz)

{{< figure src="/img/2009/09/10m.jpg" link="/img/2009/09/10m.jpg" >}}

## Measured band: filters deactivated (insertion loss)

{{< figure src="/img/2009/09/through.jpg" link="/img/2009/09/through.jpg" >}}

# Conclusions

The filters are well adjusted and perform as expected. Please note that on higher frequencies (15m and 10m) the transmission losses increase. If you don't need the filter on this band you should turn it off in order not to waste this 1,5 - 2 dB!