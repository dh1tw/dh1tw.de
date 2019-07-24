---
title: My new 40" 4K Desktop monitor (TV)
author: Tobias (DH1TW)
layout: post
date: 2017-01-13T14:07:18+00:00
url: /my-new-desktop-monitor-4k-40-inch-tv
categories:
  - Software Development
  - Hardware
tags:
  - Software Development
thumbnailImage: "img/2017/01/tvmonitor_featured.jpg"
thumbnailImagePosition: "bottom"
---

My standard development environment was for some years a 24" standard HD monitor
together with the 15" Retina display from my Macbook Pro. Recently I felt more
and more frustrated about continous window tabbing. The available screen estate
was just not enough anymore.

In my search for a bigger screen, I wondered if it wouldn't be possible to use
a 4k TV instead of a pair of > 28" PC monitors. The advantage of the 4K display
is of course its resolution of 3840px x 2160px and **much more afforable price**
than a comparable set of PC monitors.

There are several things to consider when upgrading to 4k displays, but in my
case, everything worked out well - almost out of the box. I couldn't be
happier with the result!

<!--more-->

{{< figure src="/img/2017/01/tvmonitor.jpg" link="/img/2017/01/tvmonitor.jpg" >}}


## Resultion and screen size

If you want more screen estate (more pixels), you also need the physical space
to display them somewhere. I love my Macbook's 15" Retina display, but it doesn't
provide much more screen estate than any other 15" display. Running the MPB in
its native resolution makes everything way too small. Thats why the desktop
content is scaled up to an actually sane size.

You have the same problems with any 4K display, smaller than 40". The native
resolution results in too small icons and fonts. It has to be scaled up, which
then means that your screen estate shrinks.

## The Monitor

Almost everyday, more 4K are thrown on the market. I went for the Samsung 40"
**UE40JU6500** and paid in July 2016 around 650€. It's a _curved_ TV with an
IPS panel. After having this display now in use for a couple of month, I think
the curved model is actually not worth the 100€ extra I spent on it. The IPS
panel by itself provides already a very wide viewing angle.

{{< figure src="/img/2017/01/tvmonitor2.jpg" link="/img/2017/01/tvmonitor2.jpg" >}}

## Graphics card

If you decide to go for a 4K Monitor, make sure that your graphics card
actually supports it. You will need **HDMI 2.0**, anything below won't get
you the desired result. Be aware that HDMI 1.4 can display 4K, but only at
a framerate of 30Hz. Trust me, working on a 30Hz display is not fun at all.

So you want to make sure that your graphics card is capable of full 4k,
at **60 Hz** without color compression **(4:4:4)**.

{{< figure src="/img/2017/01/tvmonitor3.jpg" link="/img/2017/01/tvmonitor3.jpg" >}}

## Connecting the Macbook to the 4K Display

The HDMI port of my Macbook Pro (Mid 2014) only supports HDMI 1.4. but
fortunately, it has 2x Mini-Displayport plugs which support 4K. I found
the a nifty Mini-Displayport to HDMI 2.0 adapter [Club 3D CAC-1170][1]
which does exactly what it promisses.
_Be aware that there are plenty of adapters out there which do not fullfill what their specs actually claim_.

Out of the box the monitor (with the adapter) was only recognized as a 4K
display in 30Hz mode. After installing [SwitchResX][2], I have 4K, 60Hz, 4:4:4
ever since :-)

## Summary

I'm more than happy with my new Setup. 3840px x 2160px provide an incredible
amount of screen estate and I barely have to switch between windows anymore.
However I had to do quite a lot of research and I probably was also a bit lucky
that the Samsung Monitor and the adapter worked almost out of the box with my
Macbook Pro.


[1]: http://amzn.eu/ihdFQdb
[2]: http://www.madrau.com