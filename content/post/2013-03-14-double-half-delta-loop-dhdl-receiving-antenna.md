---
title: Double Half Delta Loop (DHDL) Low Band Receiving Antenna
author: Tobias (DH1TW)
layout: post
date: 2013-03-14T11:22:49+00:00
url: /double-half-delta-loop-dhdl-receiving-antenna
categories:
  - Hardware
tags:
  - Antenna Simulation
  - antennas
  - Double Half Delta Loop
featured: "dhdl.jpg"
thumbnailImage: "img/2013/03/dhdl.jpg"
thumbnailImagePosition: "left"
---

A few days ago I had the time to build and try a Double Half Delta Loop (DHDL) at our Contest Station [ED1R][1]. The Antenna was built within 3 hours and can be deployed / errected within 20 minutes.

<!--more-->

## The Antenna

The Double Half Delta Loop (DHDL) was developed by George, AA7JV for his Lowband Expedition to Chesterfield (TX3A). It's a ground independent Receiving antenna which only needs two 10m support poles. Once the wires are cut and the Balun build, it takes less than 20 minutes to deploy the antenna.

A detailed description can be found at [OK1RR's website][2], the [DHDL simulation files][3] can be downloaded at TX3A website and IV3PRK's report about [two broadside phased DHDLs][4] is also worth reading.

{{< figure src="/img/2013/03/dhdl1.jpg" link="/img/2013/03/dhdl1.jpg" >}}

3D View on the Simulation Model

{{< figure src="/img/2013/03/photo_dhdl2.jpg" link="/img/2013/03/photo_dhdl2.jpg" >}}

DHDL in the backyard of ED1R

{{< figure src="/img/2013/03/photo_dhdl.jpg" link="/img/2013/03/photo_dhdl.jpg" >}}

DHDL from the feedpoint towards the second pole

{{< figure src="/img/2013/03/photo_balun.jpg" link="/img/2013/03/photo_balun.jpg" >}}

DHDL 1:18 Transformer & Resistor in their enclosures

{{< figure src="/img/2013/03/photo_dhdl_x_point.jpg" link="/img/2013/03/photo_dhdl_x_point.jpg" >}}

Supporting fibre pole in the center at 1,5m

{{< figure src="/img/2013/03/photo_dhdl_rf_choke.jpg" link="/img/2013/03/photo_dhdl_rf_choke.jpg" >}}

RF Choke at the base (25 ferrite beats) is crucial

With the specified dimensions, this non-resonant loop is optimized for 80m. On 40m, the Front/Back is too low and on 160m the signals will be very weak. The diagrams below show the patterns for 40m, 80m and 160m.

{{< figure src="/img/2013/03/dhdl_pattern_vertical.jpg" link="/img/2013/03/dhdl_pattern_vertical.jpg" >}}

{{< figure src="/img/2013/03/dhdl_pattern_horizontal.jpg" link="/img/2013/03/dhdl_pattern_horizontal.jpg" >}}

The antenna's feedpoint impedance alters between 1000 - 1200Ohm (see below). I built a 1:18 transformer on a Binocular core (Fairrite #2873000202) and terminated the loop with 1000Ohm.

{{< figure src="/img/2013/03/dhdl_impedance.jpg" link="/img/2013/03/dhdl_impedance.jpg" >}}

## Results

Despite another receiving antenna for comparison, it eliminated very well the QRM we have at ED1R on 80m Fullsize Deltaloop. On 80m I noted a very good F/B while switching between the Transmission antenna and the DHDL. As expected, on 40m the F/B was only marginal and on 160m the Signals were too weak.

**Bottom line:** The DHDL is a solid performer for 80m. On 160m a preamp is definitely required and on 40m the antenna is not that useful anymore.

## A few words of precaution

- Make sure you don't listen on the coax cable. Put sufficient ferrite beats on the coax, close to the feedpoint and close to the shack. Ground the cable in 3m distance to the feedpoint.
- Make sure that metalic structures don't disturb the antenna. Fences, Towers, Verticals in the close vicinity will create problems and couple into the DHDL. Make sure that these metal objects are at least half a wavelength away. If that's not possible you will have to de-tune your transceiving antennas - but that's another chapter.

 [1]: http://www.ed1r.com
 [2]: http://www.ok1rr.com/index.php/antennas/42-double-half-delta-loop-rx-antenna
 [3]: http://tx3a.com/docs/TX3A_DOUBLE_HALF_DELTA_LOOP.ZIP
 [4]: http://www.iv3prk.it/user/image/..-rxant.prk_tx3a.pdf