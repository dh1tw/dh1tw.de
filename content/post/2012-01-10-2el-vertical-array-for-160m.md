---
title: 2el Vertical Array for 160m
author: Tobias (DH1TW)
layout: post
date: 2012-01-10T06:40:18+00:00
url: /2el-vertical-array-for-160m
categories:
  - Contesting
  - Hardware
tags:
  - 160m
  - Antenna Simulation
  - antennas
  - Contesting
thumbnailImage: "img/2012/01/2el160m.png"
thumbnailImagePosition: "left"

---
In CQWW 160m we are planning again a serious participation. This time we want to erect a 2el vertical Array for 160m towards the US. In this post, you will find some details regarding our unique situation and some design thoughts.

<!--more-->

# ED1R Contesting site

Even while having more space than the average ham, at ED1R we are restricted when it comes to low-band antennas. Our 80m and 160m antennas have to be installed the day before the contest and be removed the night after the contest. Fortunately, the friendly neighbors allow us to use their fields during the weekends. Here is a 3D model of the ED1R contest station. Note the two (brown) areas that mark the fields we can use for our 80m / 160m antennas.

{{< figure src="/img/2012/01/ED1R_2.png" link="/img/2012/01/ED1R_2.png" >}}

## Hight is everything

When it comes to 160m, vertical antennas are hard to beat. During the last year, we used successfully (subjectively measured) a 15 tall inverted L-Antenna. The L-Antenna is a poor man's T-Antenna. The reason is that the L-Antenna has a rather significant high angle radiation which is usually not desired. On the other hand, the equally long horizontal wires of a T-antenna cancel effectively the high angle radiation.

On 160m Lambda/4 radiation is almost 40m tall. This results in an antenna radiation resistance of 36 Ohm. Unfortunately, we can't erect a 40m tall antenna. The maximum height is defined by our 18m tall Spiderbeam poles. The main problem with verticals lower than Lamdba/4 is that the antenna radiation resistance decreases. With a low antenna impedance, it is extremely important to have an excellent ground (radial) net. Otherwise, most of the power will be lost on the earth.

There are several ways to make an 18m tall antenna resonant on 160m. Here are some of the more popular designs:

1. Adding an inductor at the feed point
2. Extending the antenna with a horizontal wire (L-antenna)
3. Adding a sloping T-hat
4. Adding a horizontal T-hat

The horizontal T-hat is the best solution. With a horizontal T-hat at 18m the antenna radiation resistance, "only" drops down to approx 15 Ohm. In comparison, a sloping T-hat (two 15m long wires, sloping down at an angle of 45°) and 5mHenry at the feed point bring the antenna impedance down to 7 Ohm!

Being lucky at ED1R we have to possibility to span a long non-conductive guy-wire between the tallest tower (23m) and EC1KR's remote tower, located approximately 130m away. This allows us to install a horizontal T-hat.

## No Pain, no gain

  Since we want to seriously enter the 160m contest, we are thinking in a 2-element vertical array with the following characteristics:

  -> Two identical T-Hat Verticals
  -> 100 radials (30m long) at the feedpoint of each vertical
  -> Radial systems interconnected with a broad layer of chicken wire
  -> Optimized at 1830MHz
  -> Forced Current feeding method (Lewallen)
  -> Spacing 35m
  -> Phase: 1A, 120°
  -> Approx. 3dB Gain

Here are some pictures of how we think the antenna should look like:

{{< figure src="/img/2012/01/papa3_160m_2el_USA_view1.png" link="/img/2012/01/papa3_160m_2el_USA_view1.png" >}}

{{< figure src="/img/2012/01/papa3_160m_2el_USA_view2.png" link="/img/2012/01/papa3_160m_2el_USA_view2.png" >}}

{{< figure src="/img/2012/01/papa3_160m_2el_USA_view3.png" link="/img/2012/01/papa3_160m_2el_USA_view3.png" >}}

## Antenna pattern

The results were calculated with Mininec (good ground) and 8 Ohm losses at each feed point. The losses of the 90° feedlines were not included yet. Therefore I think a 3dB gain should be realistic.

{{< figure src="/img/2012/01/vertical-pattern.jpg" link="/img/2012/01/vertical-pattern.jpg" >}}

See above the vertical antenna pattern

{{< figure src="/img/2012/01/horizontal-pattern.jpg" link="/img/2012/01/horizontal-pattern.jpg" >}}

See above the horizontal antenna pattern of the 2el vertical array

{{< figure src="/img/2012/01/gain.jpg" link="/img/2012/01/gain.jpg" >}}

See above the gain curve for the 2el vertical array for 160m

## Comments welcome

Do you have any suggestions? The design is still not finalized yet. If you have an idea how this antenna could be improved, I would appreciate receiving your feedback!