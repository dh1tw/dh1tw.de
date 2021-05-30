---
title: Will additional coax stubs improve Bandpass Filter performance?
author: Tobias (DH1TW)
layout: post
date: 2013-05-12T21:32:42+00:00
url: /will-coax-stubs-improve-bandpass-filter-performance
categories:
  - Hardware
tags:
  - 4o3a
  - Bandpass Filter
  - ed1r
  - Measurements
  - vnwa
thumbnailImage: "img/2013/05/4o3a-filter-with-stubs.png"
thumbnailImagePosition: "bottom"

---

I was curious if the performance of our 4O3A high-power Bandpass filters could be improved with additional coax stubs in parallel. We were operating at [ED1R][2] for some time now with the added stubs, and we are pleased with the results. Check out the details!

<!--more-->

In an earlier post, I explained [how to build coaxial stubs for 20m and 40m][3]. Why 20m and 40m? A decade of hardcore contesting from stations all around the world has shown me that these two bands are the most critical ones when it comes to In-Station interferences.

## High Power Filters with additional coax stubs

{{< figure src="/img/2013/05/photo2.jpg" link="/img/2013/05/photo2.png" >}}

The picture above shows the bank of 4O3A high power bandpass filters we use are ED1R. One filter per band, from 10m to 80m. On 20m and 40m, a coaxial stub is connected in parallel to the filter's entrance, using a PL259 T-Connector.

## Results 40m

{{< figure src="/img/2013/05/4O3A-40m-Filter-with_without-Coax-Stub-and-Stub-only.png"
  link="/img/2013/05/4O3A-40m-Filter-with_without-Coax-Stub-and-Stub-only.png" >}}

_Click the diagram to enlarge_

To be honest, I was very positively surprised about the result. In the diagram above you can see the S21 attenuation of the 4O3A 40m bandpass filter (red), the coax stub only (green), and the coax stub in parallel to the Bandpass filter (blue). The coax stub adds through its sharp notch another 30db(!) on the second harmonic. The attenuation from 7MHz to 14 MHz increases from 52dB to 82dB!

## Results 20m

{{< figure src="/img/2013/05/4O3A-20m-Filter-with_without-Coax-Stub-and-Stub-only.png"
  link="/img/2013/05/4O3A-20m-Filter-with_without-Coax-Stub-and-Stub-only.png" >}}

_Click the diagram to enlarge_

This diagram shows the S21 attenuation of the 4O3A 20m bandpass filter (red), the 20m coax stub only (green), and the coax stub in parallel to the bandpass filter (blue). Again, the stub's notches on 7MHz and 21MHz improve the overall attenuation on these bands. The attenuation of 40m is kicked up from 63dB to 97dB. As a side effect, 15m gets also an additional 25dB, resulting in a total attenuation from 20m to 15m by 95dB.

## Conclusions

The 4O3A bandpass filters are doing a tremendous job at [ED1R][2]. But unfortunately, due to the direct harmonic relation of the two bands, the 20m station was still suffering severely when 40m was operating at the same time. The coax stubs give us additional attenuation between the two bands at a very inexpensive price point.

With the stubs in parallel to the bandpass filters, the interferences are still not completely gone, but at least have been reduced by another 30dB.

I can unconditionally recommend the addition of coaxial stubs in parallel to your filters if you also suffer from interferences between 20m and 40m.

 [1]: https://www.dh1tw.de/will-coax-stubs-improve-bandpass-filter-performance
 [2]: http://www.ed1r.com
 [3]: https://www.dh1tw.de/coax-stubs-for-20m-and-40m