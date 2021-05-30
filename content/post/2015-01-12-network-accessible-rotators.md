---
title: Network accessible Rotators
author: Tobias (DH1TW)
layout: post
date: 2015-01-11T23:59:47+00:00
url: /network-accessible-rotators
categories:
  - Contesting
  - Hardware
  - IT Stuff
tags:
  - antennas
  - Contesting
  - ed1r
  - Javascript
  - Node.JS
  - Ubuntu
  - Win-Test
featured: "rotator-control.png"
thumbnailImage: "img/2015/01/rotator-control.png"
thumbnailImagePosition: "left"


---
Once your contest station grows bigger and you add more antennas to turn, it becomes quite annoying to move around the physical rotator controllers between the operating positions inside the shack. Desperate for a better solution, I developed a server software that provides access to the Rotators through the network. Now all rotators can be controlled either directly through [Win-Test][1], TCP socket, or through a Web-Interface.
<!--more-->

# Server Application
During my last project [DXHeat.com][2] I learned how to write server-side Javascript with [Node.js][3]. Node.js is the server-side implementation of Google's V8 Javascript engine. Javascript is non-blocking which has the advantage that you don't have to care about Threads and parallel processes. Within the big ecosystem of Node.js, I found a suitable module for accessing [serial ports][4]. Everything else (TCP, UDP servers) comes with the Node.js core libraries.


## Rotators & USB

At [ED1R][5], all our rotators are connected to [EA4TX's superb ARS control units][6]. Besides providing a slick User Interface, ARS also provides a USB interface.

## Server Hardware

We stuffed into an old Pentium 4 server two PCI cards which offer 4 USB ports each. Due to RF interferences in earlier contests, we bought high-quality, double-shielded USB cables from [Lindy](http://www.amazon.de/gp/product/B001G5VII6?psc=1&redirect=true&ref_=oh_aui_detailpage_o02_s00). We choose Ubuntu 14.04 as the operating system. Since Node.js is cross-platform, I&#8217;m sure that the application could also run under Windows. But why bother, Ubuntu is a great and free Operating System.

## Internals

I tried to keep the software as modular as possible. Through a config file, an arbitrary amount of Rotators (/dev/ttys) can be specified. On application start, each rotator will be registered within the network and a TCP port is opened. I wrote a small Library that broadcasts UDP messages in the Win-Test format so that the rotators automatically appear within each Win-Test Instance. Communication with the Web-Interface is handled through a Websocket, using [socket.io][7]. Since fault tolerance was very important (e.g. RF interferences), the software can detect a non-responsive rotator, remove it, and load it, once it becomes again available **without** affecting the other rotators. Find below an example of our configuration file.

{{< figure src="/img/2015/01/arsctl_config.png" link="/img/2015/01/arsctl_config.png" >}}

# GUI Applications & Integration

I wrote a small Web Application that allows to conveniently change the antenna direction by point&click on the compass rose. The yellow arrow represents your PRESET and disappears, once the rotator (red) has reached the desired heading. Since we have distributed our antennas on several towers, it was also important to see at a glance where the remaining antennas are heading to. All graphical parts were done using [HTML5 canvas][9]. Communication from the Web-App with the server is done through the client library of [socket.io][7]. Again, fault tolerance is built-in. If a rotator fails, the button & compass rose of the affected rotator just disappear until the rotator becomes available again.

{{< figure src="/img/2015/01/arsctl_gui.png" link="/img/2015/01/arsctl_gui.png" >}}

# Source Code

I published the software under the [GPL][11] license. The source code with installation instructions is available on my [Github Profile][12]. Feel free to fork it! The software has been written for Mac OS and Ubuntu systems. But it should be possible to run the code with small modifications also on other Linux distributions and Windows. It works like a charm on Raspberry Pi devices!

# Resume

Finally, we are now able at [ED1R][5] to control all antennas conveniently from any of our 5 operating positions without moving the bulky Yaesu control units anymore. The GUI application shows you immediately the heading direction of all our antennas. Thanks to the Win-Test integration, it has never been so easy to rotate our antennas. By typing in a callsign and pressing CTRL-F12, the antenna now moves directly into your QSO partner's direction.

 [1]: http://www.win-test.com
 [2]: https://dxheat.com
 [3]: http://nodejs.org
 [4]: https://github.com/voodootikigod/node-serialport
 [5]: http://www.ed1r.com
 [6]: http://www.ea4tx.com
 [7]: http://socket.io
 [9]: http://www.w3schools.com/html/html5_canvas.asp
 [11]: http://www.gnu.org/licenses/gpl-3.0.de.html
 [12]: https://github.com/dh1tw/arsctl
