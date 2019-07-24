---
title: PowerSDR-UI – knobs for your SDR radio
author: Tobias (DH1TW)
layout: post
date: 2011-03-12T12:00:38+00:00
url: /powersdr-ui
categories:
  - Hardware
  - Software Defined Radio
tags:
  - PowerSDR
  - powersdr-ui
  - Software Defined Radio
  - user interface
thumbnailImage: "img/2011/03/iStock_000004875670XSmall.jpg"
thumbnailImagePosition: "left"

---
At the end of last year I announced the "proof" that Software Defined Radios also can have buttons and knobs. At that stage the software was still a prototype and not ready for a public release. In the meantime I was working hard to eliminate bugs and implement further improvements. By today I'm happy to announce the release of PowerSDR-UI beta. This is a call for beta testing. Please feel free to download the software and participate in the beta testing phase!
<!--more-->

## Description

PowerSDR-UI  is a fork of  FlexRadio Systems *PowerSDR*. It comes with all the features and bugs of that version but with one important difference: Support of an inexpensive, versatile User Interface with real knobs, sliders and buttons. On each element of the User Interface, a function of PowerSDR can be mapped (e.g. AF Gain, Filter Width,...etc). A detailed description can be found in the article I wrote about [why current SDR solutions lack of a proper User Interfaces](https://www.dh1tw.de/disc-jockeys-influence-on-sdr).

The following two videos have been created by PowerSDR-UI users and demonstrate the integrated DJ Console with PowerSDR:

English:

{{< youtube B-Qp2mMdAt0 >}}

Japanese:

{{< youtube ENPfLtsEcMk >}}

## Release note

PowerSDR-UI is currently at beta status. This means that it is not perfect and that errors might appear. The intention of this release is to get feedback from the community with their various SDR based radios.

From a licensing point of view it is important to understand that FlexRadio Systems has divided PowerSDR in two parts. The application PowerSDR is open source (GPL license) but various drivers are closed source and may not be distributed by third parties (here: me, DH1TW). This is the reason why I can not offer an automated installer as you would expect from any program today. Instead a bit of manual work is needed. But with basic PC knowledge and the installation instruction below I'm sure you will be able to install PowerSDR-UI.

The content of the PowerSDR-UI Zip file is:

- PowerSDR-UI x.xx.exe
- Sanford.Collections.dll
- Sanford.Multimedia.dll
- Sanford.Multimedia.Midi.dll
- Sanford.Threading.dll

The DLLs are part of the [C# MIDI Toolkit](http://www.codeproject.com/KB/audio-video/MIDIToolkit.aspx) which I'm using to communicate with the various DJ Consoles.

The following functionality can be mapped onto **buttons**:

* A > B
* A < B
* A <> B
* Split
* 0 Beat
* RIT
* XIT
* Clear RIT
* Clear XIT
* MultiRx
* VFO Sync
* VFO Lock
* MOX
* VOX
* Mute
* NB1
* NB2
* ANF
* NR
* SR
* BIN
* Wider Filter
* Narrower Filter
* Next Mode
* Prev Mode
* Tuning Step Up
* Tuning Step Down
* Band Up
* Band Down
* Start
* Tuner
* CPDR
* DX
* DEXP
* RX2 On/Off
* RX2 PreAmp
* RX2 NB1
* RX2 NB2
* RX2 Band Up
* RX2 Band Down
* Enable Rx EQ
* Enable Tx EQ
* Squelch
* BCI Rejection
* AGC Mode Up
* AGC Mode Down
* Preamp (Flex5000)
* AVG
* Peak
* Show TX Filter
* Display Mode Next
* Display Mode Prev
* Zoom Step Up
* Zoom Step Down
* Quick Mode Save
* Quick Mode Restore
* Send CWX Macro 1
* Send CWX Macro 2
* Send CWX Macro 3
* Send CWX Macro 4
* Send CWX Macro 5
* Send CWX Macro 6
* Send CWX Macro 7
* Send CWX Macro 8
* Send CWX Macro 9
* Stop Sending CWX Macro (immediately)
* MON
* Center Pan Slider
* VAC On/off
* I/Q to VAC1
* I/Q to VAC1 use RX2
* VAC2 On/Off
* ESC On/Off
* ESC Form Open/Close
* Mute RX2
* TUN
* Tuner Bypass
* 160m
* 80m
* 40m
* 30m
* 20m
* 17m
* 15m
* 12m
* 10m
* 6m
* 2m
* 160m RX2
* 80m RX2
* 40m RX2
* 30m RX2
* 20m RX2
* 17m RX2
* 15m RX2
* 12m RX2
* 10m RX2
* 6m RX2
* 2m RX2
* Mode SSB (automatically selects USB/LSB
* Mode LSB
* Mode USB
* Mode DSB
* Mode CWL
* Mode CWU
* Mode DIGU
* Mode DIGL
* Mode SPEC
* Mode AM
* Mode FM
* Mode DRM
* Mode SAM


The following functionality can be mapped onto **potentiometers**:

* RIT
* XIT
* Shift
* AF Gain
* Volume Rx1
* Volume Rx2
* Ratio Main/Sub Rx
* PreAmp Settings
* CW Speed
* AGC Threshold
* Drive Level
* Mic Gain
* CPDR Threshold
* Vox Gain
* DEXP Threshold
* Squelch Threshold
* AGC Threshold RX2
* TX AF Monitor
* AGC Mode
* Zoom Slider
* Volume RX2
* Pan RX2
* VAC RX Gain
* VAC TX Gain
* VAC2 RX Gain
* VAC2 TX Gain
* Waterfall / Grid Low Limit
* Waterfall / Grid High Limit
* Stereo Balance RX2 (PAN)

The following functionality can be mapped onto **rotary pulse encoders**:

* Frequency VFOA
* Frequency VFOB
* Filter Bandwidth
* RIT
* Zoom Slider
* Upper Edge of DSP Filter
* Lower Edge of DSP Filter
* PAN Slider


## Supported devices

1. [Hercules DJ Control MP3 LE](http://www.amazon.com/gp/product/B008YDU1DG/ref=as_li_qf_sp_asin_tl?ie=UTF8&#038;tag=dhde-20&#038;linkCode=as2&#038;camp=1789&#038;creative=9325&#038;creativeASIN=B008YDU1DG)

2. Hercules DJ Console MP3e2 (not sold anymore)
3. Hercules DJ Console MK2 (not sold anymore)

## Download

PowerSDR-UI has been deprecated. The code has been donated to serveral authors
of other forks. Please check out [KE9NS' fork](https://www.ke9ns.com/flexpage.html).

 [1]: http://groups.yahoo.com/group/PowerSDR-UI/
 [2]: https://www.dh1tw.de/how-powersdr-ui-users-set-up-their-dj-consoles