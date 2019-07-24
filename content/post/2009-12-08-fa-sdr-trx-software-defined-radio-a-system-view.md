---
title: 'FA-SDR-TRX part #1 – Systems View'
author: Tobias (DH1TW)
layout: post
date: 2009-12-08T21:18:25+00:00
url: /fa-sdr-trx-software-defined-radio-a-system-view
categories:
  - Software Defined Radio
tags:
  - fa-
  - Funkamateur
  - kit
  - Software Defined Radio
thumbnailImage: "img/2009/11/FA-SDR-TRX-Software-Defined-Radio-PCB.jpg"
thumbnailImagePosition: "left"

---
The [FA-SDR-TRX](https://www.dh1tw.de/fa-sdr-trx-funkamateur-allband-sdr) is an allband low cost software defined radio. The FA-SDR-TRX was created by Harald DL2EWN an described in an article series in the German Ham Radio Magazine Funkamateur. After the big success of the single band kits like Softrock, SDR4080 or Genesis, the FA-SDR-TRX is the next step in the evolution of SDR kits. Thanks to the support of Harald I'm able to provide a detailed description of the concept behind FA-SDR-TRX.
  <!--more-->

### Other posts in this series:

[FA-SDR-TRX - part #1 - a Systems View](../fa-sdr-trx-software-defined-radio-a-system-view)

[FA-SDR-TRX - part #2 - the Receiver](https://www.dh1tw.de/software-defined-radio-fa-sdr-trx-receiver)

[FA-SDR-TRX - part #3 - the Transmitter](https://www.dh1tw.de/software-defined-radio-fa-sdr-trx-transmitter)

# Motivation

Harald, DL2EWN's motivation was to create a software defined radio platform which can receive and transmit on all amateur HF bands (160m-10m). The receiver shall have very good characteristics and the transmitter shall be capable to deliver a clean 1 Watt signal for a serious usage on the bands. The whole transceiver shall be located on a single PCB, but maintaining the flexibility to use the receiving part without having assembled the transmitting path. Having in mind that the FA-SDR-TRX will be assembled by a lot of Hams with different skills, reproducibility of it's performance was an important requirement. Even if the kit contains SMD components, all of them will be pre-mount on the PCB to simplify assembly. A modular design and the use of inexpensive and widely available components shall ensure an affordable price.

# Concept

The fundamental components of the FA-SDR-TRX are illustrated in the drawing below:

{{< figure src="/img/2009/12/FA-SDR-TRX-Overview1.png" link="/img/2009/12/FA-SDR-TRX-Overview1.png" >}}

The transceiver consists out of the 7 major components:

1. ATT – Attenuator
2. BPF – Band Pass Filter / Preselector
3. BUFFER AMP – Buffer Amplifier (actually its part of the preselector)
4. GEN – Signal Generator
5. MIXER Rx – Quadrature Sampling Detector (QSD)
6. Mixer Tx – Quadrature Sampling Exciter (QSE)
7. AMP – an optional 1Watt amplifier

The FA-SDR-TRX provides the following interfaces:

1. RF Input – Antenna Signal
2. Audio RX – Receiving stereo IQ signal – to be connected to LineIn on the Soundcard
3. Audio TX – Transmission stereo IQ signal – to connected to LineOut on the Soundcard
4. USB – Tuning the Frequency, CW Signal and PTT
5. CW – External CW Key

# Shared components

The FA-SDR-TRX is sharing some of it's components between the receiving and the transmitting path. The following drawing shows the grouped components.

{{< figure src="/img/2009/12/FA-SDR-TRX-structure.png" link="/img/2009/12/FA-SDR-TRX-structure.png" >}}

Attenuator and RX Mixer are exclusively used by the RX path. Amp and TX Mixer are used exclusively by the TX path. Bandpassfilter, Buffer-Amp and the Signal Generator however are shared components. They are used by both, the RX and TX path.

# Block Diagram

This block diagram shows the interaction between the components:

{{< figure src="/img/2009/12/FA-SDR-TRX-with-RX-and-TX-path.png" link="/img/2009/12/FA-SDR-TRX-with-RX-and-TX-path.png" >}}

Please note that this is a simplified view

## FA-SDR-TRX Receiver

So, lets get into more detail. We'll start with the receiving part of the FA-SDR-TRX. Meanwhile, the Transmission path is greyed out.

{{< figure src="/img/2009/12/FA-SDR-TRX-with-RX-path.png" link="/img/2009/12/FA-SDR-TRX-with-RX-path.png" >}}

The RF Signal is fed into an attenuator. Even if the overall performance of the receiver is very good (IP3  >15dBm [actually IP3 would be +28dBm without the buffer amp] and IMDR3 >90dB) an attenuator was implemented to avoid overloading the receiver with too strong signals (e.g. 49m band). Passing the attenuator, the Signal is filtered in an adjustable bandpassfilter / preselector. The following buffer amp (SGA5289) ensures a 50Ohm match to the following stage and suppresses unwanted radiation of the QSD's switching frequency. The amplifier is an MMIC with 13dB gain.  The following Mixer is a Quadrature Sampling Detector providing the IQ baseband signal for the soundcard. Several classical switching-ICs (FST3253, MAX4614, 74HC4066) were tested. The, still quite unknown 74LVC4066 showed the best results. Making maximum use of existing components, the proven FA-SY1 generator (Si570) was implemented. The FA-SY1 provides a USB interface to tune the frequency.

##  FA-SDR-TRX Transmitter

The next illustrations shows the transmission path of the FA-SDR-TRX.

{{< figure src="/img/2009/12/FA-SDR-TRX-with-TX-path.png" link="/img/2009/12/FA-SDR-TRX-with-TX-path.png" >}}

With the help of a PC and it's soundcard, an IQ (stereo) Signal is fed into the TX-Mixer. The frequency of the Quadrature Sampling Exciter is tuned with the Si570 generator (the same which is used by the RX). At this stage, the output power of the QSE is about 1mW. Unwanted Harmonics and intermodulation products are suppressed by the passive preselector. The buffer amp boosts the "cleaned" signal to 10mW. Intermodulation products are with -56dBc well below the carrier. Image frequency surpression is with -60dBc also ok. Before sending the signal on the air, the FA-SDR-TRX allows the use of a 1-Watt amplifier (RD00HHS1 MOSFETs). This amplifier is optional and realized with an additional PCB which can be plugged in the FA-SDR-TRX PCB. However this Amplifier is not part of the FA-SDR-TRX kit. It has to be purchased separately.

# Stay tuned

I hope that this article gave you an overview about the concept behind this allband software defined radio. kit. In further article I'll explain the mentioned components in greater depth. Maybe IÄll also be able to provide the schematics, but this has to authorized by the publisher Funkamateur.

Kits will be available in January 2010. Orders are already taken. If you are interested, you might consider to place an order. Usually the first batch of Funkamateur kits are sold out early after the release. The kit is called BX200 and costs 124€ (approx. 180 USD). Please note that the Si570 Signal Generator (FA-SY1) and the 1-Watt Amplifier (not available so far) have to be purchased apart.