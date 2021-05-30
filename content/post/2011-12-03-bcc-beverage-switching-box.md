---
title: Building a beverage switching box
author: Tobias (DH1TW)
layout: post
date: 2011-12-03T00:21:04+00:00
excerpt: "For CQWW CW Contest I've built up a Beverage switching box which allows the simultaneous reception on 6 beverages across 40m, 80m and 160m at the same time"
url: /bcc-beverage-switching-box
categories:
  - Hardware
tags:
  - Bandpass Filter
  - BCC
  - beverage antennas
  - Contesting
  - Filter
  - Measurements
  - TAPR VNA
thumbnailImage: "img/2011/12/beverage_box.jpg"
thumbnailImagePosition: "left"
---

This year we wanted to seriously compete in CQWW CW from the ED1R contest station. While the station is equipped reasonably on all bands with Yagis and verticals, there were no dedicated receiving antennas available - yet. Out of my former contest participation from other stations, I know that when it comes down to winning a CQWW, dedicated receiving antennas are a must-have. Beverages provide great directivity and reduce the EU clutter significantly.

<!--more-->

## Making things happen

Apart from the two running stations, we planned to operate an additional Multiplier station. So during nighttime, three stations would need to use the same beverages simultaneously. At that point, I decided to build up a Beverage distributor. My friends Ben, DL6RAI, and Ulli, DK4VW from the [Bavarian Contest Club](http://www.bavarian-contest-club.de) published more than a decade ago a great design which has been proven to work during the various Multi/Multi expeditions of the BCC, including the World-Record as [CN8WW](http://www.dl6fbl.de/cn8ww). All the details were published in a [CQ Magazine
article](http://www.bavarian-contest-club.de/projects/bevbox.pdf).

## Requirements

  1. Six receiving antennas shall be switchable to three stations (40m, 80m, 160m)
  2. All three stations shall be able to listen to any antenna they want at any time
  3. There shall be no influence and restriction between the three stations
  4. Remote control and the RF signals shall be done with just one cable

## Design & Assembly

[Patrick, TK5EP](http://tk5ep.free.fr/tech/beverage/bevtheory.htm) has documented his version of the BCC Beverage distributor on his website and I can highly recommend following his design.

Since there were no more PCB designs available I created my own. I used the standard design with an LM3914 but instead of driving each relay with a dedicated transistor, I used a ULN2003 Darlington array IC. The PCBs were manufactured by [Olimex](http://www.olimex.com) in Bulgaria. They have a turn-over time of 3-5 days and the total cost of a double side PCB, incl solder mask and component print is just 30 € (excluding shipping & VAT). The shipment with FedEx took less than 24 hours!!!

The reason why we can listen on the same antennas on 40m, 80m, and 160m in parallel is due to the fact of using bandpass filters for each band. The bandpass filters are designed to have 50 Ohm impedance in their transmission band but have a high impedance outside of their transmission bands.

Example: Having 50 Ohm in parallel with 50 Ohm has a high impact and result in 25 Ohm. But having 50 Ohm in parallel with 1500 Ohm results in 48,4 Ohm which is rather negligible. That's why we can connect the three bandpass filters in parallel with almost no influence between them.

The Box itself is still not finished, but we successfully burnt it in during the CQWW CW finishing with 15% over the old European M/2 record of [RU1A](http://www.ru1a.ru).

Here are some pictures:

{{< figure src="/img/2011/12/photo.jpg" link="/img/2011/12/photo.jpg" >}}

The picture above (click to enlarge) shows the S21 curves of the 40m (blue), 80m (green), and 160m (pink) beverage filter. Measurements were performed with a [DG8SAQ VNWA](http://www.sdr-kits.net/VNWA/VNWA_Description.html). The bandpass filters have a passband attenuation of approximately 0.5dB - 1.5 dB which is ok since the Beverage itself is a lossy antenna.

{{< figure src="/img/2011/12/beverage-160m-bandpass-filter_with_Z.png"
  link="/img/2011/12/beverage-160m-bandpass-filter_with_Z.png" >}}

The filter plot above (click to enlarge) shows the S11 (blue), S21 (black), and absolute Impedance (pink) of the 160m filter. Note that the 160m has an absolute impedance of 500 Ohm on 3,5MHz and 1600 Ohm on 7 MHz.

{{< figure src="/img/2011/12/photo.jpg" link="/img/2011/12/photo.jpg" >}}

The picture above shows the three bandpass filters. For all coils, a stack of three cores (Amidon T68-2 or T68-6) was used. If you want to calculate coils I can warmly recommend the free software [MiniRingkern-Calculator](http://www.dl5swb.de/html/mini_ringkern-rechner.htm) published by DL5SWB. I'm using SMA connectors. They are a bit expensive but make it easy to connect to the Network Analyzer.

Last but not least, here are a few detailed pictures of the PCB / PCB stack and the overall assembly:

{{< figure src="/img/2011/12/photo7.jpg" link="/img/2011/12/photo7.jpg" >}}

Assembled PCB

{{< figure src="/img/2011/12/photo5.jpg" link="/img/2011/12/photo5.jpg" >}}

A total of three PCBs are needed - one for each band

{{< figure src="/img/2011/12/photo6.jpg" link="/img/2011/12/photo6.jpg" >}}

The three PCBs are connected through wires

{{< figure src="/img/2011/12/photo4.jpg" link="/img/2011/12/photo4.jpg" >}}

The PCB stack is mounted with distance bolts on top of the bandpass filter

{{< figure src="/img/2011/12/photo2.jpg" link="/img/2011/12/photo2.jpg" >}}

Cables (PTFE - Teflon) are soldered directly onto the PCB

{{< figure src="/img/2011/12/photo1.jpg" link="/img/2011/12/photo1.jpg" >}}

Here is a picture of the Beverage switching box in action at <a href="http://www.ed1r.com/">ED1R</a>. All we had to do was manually allocating the station's receiving cable to the appropriate band (through connecting the station's cable to the appropriate BNC plug).

{{< figure src="/img/2011/12/26112011-038.jpg" link="/img/2011/12/26112011-038.jpg" >}}

{{< figure src="/img/2011/12/26112011-068.jpg" link="/img/2011/12/26112011-068.jpg" >}}

Each station has its remote control to select the proper listening antenna. Here are two more pictures:

{{< figure src="/img/2011/12/26112011-025.jpg" link="/img/2011/12/26112011-025.jpg" >}}

Since we had only two beverages available they were labeled "EU" and "NA". Each station had the same control unit. The remaining four (unlabeled) positions of the switch are unused.

{{< figure src="/img/2011/12/Photo-on-12-3-11-at-1.07-AM.jpg"
  link="/img/2011/12/Photo-on-12-3-11-at-1.07-AM.jpg" >}}

The picture above shows the network of resistors that are used to select one of the six beverages through the LM3914 IC in the Beverage switching box. The RF signal is decoupled from the DC signal through a 1nF ceramic capacitor.

## Conclusions

The [BCC](http://www.bavarian-contest-club.de) Beverage switching box worked as expected. During the CQWW CW, we could significantly increase our score. In total 20% more than the SSB team and 15% above the old European Multi/2 record. The beverage switch worked reliable and has already been considered after one contest as a fix station asset 🙂

**Update 1.6.2012:** In the meanwhile I've updated the PCB design and manufactured a second version which eliminated some small mistakes.

## Want to build your own?

in case you are interested in building your Beverage switching box, then feel free to contact me about PCBs.