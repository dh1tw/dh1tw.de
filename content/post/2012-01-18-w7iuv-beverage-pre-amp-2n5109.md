---
title: W7IUV Beverage Pre-Amp (2N5109)
author: Tobias (DH1TW)
layout: post
date: 2012-01-18T11:48:59+00:00
url: /w7iuv-beverage-pre-amp-2n5109
categories:
  - Contesting
  - Hardware
tags:
  - amplifier
  - Bandpass Filter
  - beverage antennas
  - Contesting
  - Measurements
  - w7uiv amplifier

---
In preparation for the upcoming CQWW 160m Contests, my friend [Hannes, DK1NO](http://qrz.com/db/dk1no) was so kind to give me one of his W7IUV broadband, high IP3 preamplifier. Thanks, Hannes! Without knowing the exact performance data, I ran a few measurements with my Network Analyzer on the amplifier to determine the Gain and its operational fitness. Read on for measurement results and additional notes on how to measure active components.

<!--more-->

In the pictures below, the measurement setup can be seen. I'm using a high-precision [USB Network Analyzer](http://sdr-kits.net) made by DG8SAQ (90dB dynamic range), a Mini-Circuits BNC Calibration kit, and some Mini-circuits attenuators.

A few notes on measuring amplifiers:


*  When measuring active components on a network analyzer DC must not be applied at any time at the Network Analyzer's input terminals. Just with a few Volts, you can brick your (expensive) measurement devices. A good way to make sure that DC reaches the VNWA's terminals is to use a coupling capacitor.

* Amplifiers can easily overload your VNWAs input terminals. Caution is needed, especially if the gain is unknown, as in my case. My VNWA allows me to reduce the output power in 0.1 dB steps, therefore I started with -40dBm and added a 20dB attenuator at the receiving port, just to make sure that no overloading will happen.

{{< figure src="/img/2012/01/IGP8042.jpg" link="/img/2012/01/IGP8042.jpg" >}}

Measurement setup: Regulated Powersupply (with current limiter), USB Vector Network Analyzer, and the W7IUV amplifier

{{< figure src="/img/2012/01/IGP8044.jpg" link="/img/2012/01/IGP8044.jpg" >}}

A closer look at the VNWA and the W7IUV Beverage Amplifier

{{< figure src="/img/2012/01/IGP8043.jpg" link="/img/2012/01/IGP8043.jpg" >}}

A detailed picture of the W7IUV Beverage Pre-Amplifier. Note the 20dB attenuator at the output port

{{< figure src="/img/2012/01/Messung-DK1NO-Beverage-Preamp-100MHz.png"
  link="/img/2012/01/Messung-DK1NO-Beverage-Preamp-100MHz.png" >}}

The amplifier shows satisfactory behavior. Over the whole shortwave band  (1MHz - 30MHz) the gain (S21) is 20dB, decreasing to approx. 8dB at 100MHz. Also, the input impedance (S11) is good from 1 MHz to 30MHz.

Overall I'm happy with the gain and the input impedance. Of course, a few other important measurements (e.g. IP3) are missing. Since I don't have the necessary means to measure the IP3 I'll accept the amplifier as is. For the contest, I'll put the Amplifier behind a Lowpass / Bandpass filter just to make sure that no unnecessary intermodulation products are generated.