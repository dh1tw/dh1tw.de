---
title: Can I still use oxidized coax cable?
author: Tobias (DH1TW)
layout: post
date: 2013-03-18T02:24:55+00:00
url: /can-i-still-use-oxidized-coax-cable
categories:
  - Hardware
tags:
  - coax-cable
  - Measurements
thumbnailImage: "img/2013/03/oxidized_cable.jpg"
thumbnailImagePosition: "left"
---

This question bugged me after trying to exchange the connectors of a 25m long Aircell7 coax cable. During preparation I discovered a black inner conductor. I seems water entered the cable. Do I have to throw it away? Read more to discover a probably unexpected answer!

<!--more-->

## Water in the Cable

It's the nightmare of all hams: water inside the coax cable. Over years, I heard over and over that once water has entered the cable, it becomes useless and has to be thrown away. From my times at university I remembered that due to the  _Skin Effect_, RF energy tends to flow on the skin, rather than the inner core of the conductor. Since copper oxide conducts much worse than copper, theory seems to confirm the country saying.

But considering the price of 2,50€/m I felt a stich in my heart when thinking about throwing away this 25m role of [Aircell7][1]. Instead of accepting defeat, I pulled out my [Vector Network Analyzer][2] and measured the attenuation from 1-500MHz.

## Oxidized coax cable

{{< figure src="/img/2013/03/oxidized_coax_cable.jpg" link="/img/2013/03/oxidized_coax_cable.jpg" >}}

It seems water entered from one side of the coax cable. While I had to cut off 2 meters to reach the part of the cable where the shield was not oxidized anymore, the inner conductor was completely oxidized from the beginning to the end.

## Measuring attenuation

{{< figure src="/img/2013/03/Aircell7-245m-oxidierter-Innenleiter.png"
  link="/img/2013/03/Aircell7-245m-oxidierter-Innenleiter.png" >}}

Before measuring S21 attenuation I scratched of the copper oxide and put tin-solder on the ends to ensure a proper contact. Surprisingly, the results where much better than expected!

<table border="1" cellspacing="1" cellpadding="10">
  <tr>
    <th>
    </th>

    <th>
      Manufacture's specification [25m]
    </th>

    <th>
      Measured values [25m]
    </th>
  </tr>

  <tr align="center">
    <td>
      10MHz
    </td>

    <td>
      0,5dB
    </td>

    <td>
      0,6dB
    </td>
  </tr>

  <tr align="center">
    <td>
      30MHz
    </td>

    <td>
      1,0dB
    </td>

    <td>
      1,2dB
    </td>
  </tr>

  <tr align="center">
    <td>
      144MHz
    </td>

    <td>
      1,9dB
    </td>

    <td>
      2,4dB
    </td>
  </tr>

  <tr align="center">
    <td>
      432MHz
    </td>

    <td>
      3,4dB
    </td>

    <td>
      <b><font color="red">10,3dB</b></font></td> </tr> </table>

## Results
Will I throw the cable in the trash can? No! Below 30MHz, the attenuation increased with 0,2dB only marginally. Even on 144MHz it could still be used in an emergency situation. Only above, the skin effect really starts to be noticeable. With 7dB additional attenuation of 432MHz, it's definitely not suitable for UHF anymore.

I hope this measurement might also helps you to take the right decision when you find next time a coax cable with an oxidized inner conductor. I didn't expect this result. I just saved 50€ and will continue using the cable on Shortwave.

 [1]: http://www.kabel-kusch.de/Koaxkabel/SSB-Kabel/aircell7.htm
 [2]: https://www.dh1tw.de/evolution-of-the-dg8saq-vnwa