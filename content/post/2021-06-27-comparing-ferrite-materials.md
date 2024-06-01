---
title: "What's the best ferrite material for a common-mode choke?"
author: Tobias (DH1TW)
date: 2021-06-27T12:00:00+02:00
layout: post
categories:
  - Hardware
  - EMC
tags:
  - ferrite
  - emc
thumbnailImage: "img/2021/06/ferrite_teaser.jpg"
thumbnailImagePosition: "bottom"
---

Sometimes household appliances cause (significant) electromagnetic interferences in our receivers. Unfortunately, replacing them isn't always an option. Fortunately, adding common-mode chokes to the input and/or output cables can drastically reduce the emitted interferences. Choosing the right ferrite material is probably the most important success factor. In this post, I compare three different materials and show how you can measure and evaluate (random) ferrite cores by yourself!

<!--more-->

## The Ferrite cores under test

I like the ferrite cores with a diameter of approximately 40mm. This size is an excellent trade-off between the number of turns I can wind onto it and the price/core. If you install a lot of cores around your house, this can get easily quite expensive. In the past I used [TDK R40 N30](https://www.tdk-electronics.tdk.com/download/187204/11a3ca92549b8d3b7cce210eace3dc3c/pdf-n30.pdf), [Amidon FT140-43](http://www.amidoncorp.com/ft-140-43/) and [Thora TF-135 split conductor cores](https://www.buerklin.com/medias/sys_master/root/hd7/h7e/9282700673054/8866501656606.pdf) with good success. However, I never measured the characteristics of the individual ferrite material. I mainly trusted friends who recommended them. When I recently got some [Würth 4727015 cores (4W620 material)](https://www.mouser.de/datasheet/2/445/7427015-1720537.pdf) for a bargain, I decided to take the chance and compare the three similar cores properly.

On each core, I wound 8 turns of 24 AWG wire. 8 turns represent the average of what can be easily wound on a ferrite core with a 40mm diameter using PVC cable / [NYM-J cable](https://de.wikipedia.org/wiki/Kennzeichnung_von_Leitungen_und_Kabeln#Kennzeichnung_gem%C3%A4%C3%9F_deutschen_Normen) with 2-3x 0.75mm² - 2.5mm² conductor cross-section.

{{< figure src="/img/2021/06/tdk_r40_n30_wuerth_7427015_amidon_ft140-43.jpg"
    link="/img/2021/06/tdk_r40_n30_wuerth_7427015_amidon_ft140-43.jpg"
    caption="The ferrite cores under test - TDK R40 N30, Würth 7427015 and Amidon FT140-43">}}

## What to measure

The most important parameter is the [insertion loss (S21)](https://en.wikipedia.org/wiki/Scattering_parameters#Insertion_loss). The more the choke attenuates the common-mode signals on the cable, the better. Knowing the impedance |Z|, and its resistive Rs and reactive |Xs| components are also desirable. Steve, G3TXQ (SK) explains in-depth on his website [why predominantly resistive common-mode chokes Rs>|Xs| are better](http://www.karinya.net/g3txq/chokes/). 

## How to measure

For measuring S11 and S21 we ideally use a Vector Network Analyzer. Luckily, these days you can already get [nanoVNA](https://nanovna.com/) for less than 100 USD. For my measurements, I used my trusted [DG8SAQ VNWA](https://www.sdr-kits.net/DG8SAQ-VNWA-software-documentation-user-guide). For measuring the impedance (S11) I added an SMA plug to each choke. For measuring insertion loss (S21) I built a ground plane with crocodile clips connected to an N-plug.

{{< figure src="/img/2021/06/insertion_loss_test_jig.jpg"
    link="/img/2021/06/insertion_loss_test_jig.jpg"
    caption="convinience test jig for measuring insertion loss (S21)">}}

## Individual measurements

The figures for each of the individual measurements is a combined chart of the following values: 
- Insertion Loss (red)
- Impedance |Z| (blue)
- Resistive Impedance Rs (pink)
- Reactive Impedance Xs (orange)

The scale and reference for the impedances are the same (500 Ohm/unit). The scale can be found on the left side of the Y-axis. For the insertion loss, a scale of 5dB has been chosen. The scale is located on the right side of the Y-axis.

### TDK N30 R40

{{< figure src="/img/2021/06/tdk_n30_r40_8_turns.png"
    link="/img/2021/06/tdk_n30_r40_8_turns.png"
    caption="Measured impedance (S11) and insertion loss (S21) of an 8 turn common-mode choke on a single TDK N30 R40 ferrite core">}}

From the insertion loss, we can see, that the N30 ferrite material from TDK is an excellent choice for lower frequencies. The attenuation decreases continuously over frequency. Over the entire short wave range, the impedance is predominantly resistive. 

### Amidon FT140-43

{{< figure src="/img/2021/06/amidon_ft140-43_8_turns.png"
    link="/img/2021/06/amidon_ft140-43_8_turns.png"
    caption="Measured impedance (S11) and insertion loss (S21) of an 8 turn common-mode choke on a single Amidon FT140-43 ferrite core">}}

The plotted insertion loss starts with a meager 10dB around 1MHz. However, over frequency, the insertion loss increases continuously. The "dip" around 75MHz is most likely due to a resonance in my test jig and should be ignored. Over the first couple MHz, the choke is almost entirely reactive but becoming predominantly resistive between 8...35 MHz.

### Würth 7427015

{{< figure src="/img/2021/06/wuerth_7427015_8_turns.png"
    link="/img/2021/06/wuerth_7427015_8_turns.png"
    caption="Measured impedance (S11) and insertion loss (S21) of an 8 turn common-mode choke on a single Würth 7427015 ferrite core">}}

To my surprise, the characteristics looked almost identical to the ones of Amidon FT140-43 choke. Please ignore the insertion loss "dip" around 80MHz. I'm sure it's caused by a resonance of this choke in combination with the test leads of my jig.

## Comparisions

The following two charts show the impedances and insertion loss of the three ferrite cores in a combined chart. The colors identify the ferrite cores: 
- TDK N30 R40 (green)
- Amidon FT140-43 (blue)
- Würth 7428015 (red)

### Impedances

In the following chart the impedances |Z| of the three cores are shown:

{{< figure src="/img/2021/06/8_turns_ft140-42_N30R40_7427015_10MHz_impedance.png"
    link="/img/2021/06/8_turns_ft140-42_N30R40_7427015_10MHz_impedance.png"
    caption="Measured impedances |Z11| of an 8 turn choke on TDK N30 R40, Amidon FT140-43 and Würth 7427015">}}

Now it becomes clear, that the Würth 4W620 material has almost the same characteristics as Amidon's 43 material. TDK's N30 material is a different mixture and provides impedances on the low bands.

### Insertion loss

In the following chart the impedances |Z| of the three cores are shown:

{{< figure src="/img/2021/06/8_turns_ft140-42_N30R40_7427015_100MHz_insertion_loss.png"
    link="/img/2021/06/8_turns_ft140-42_N30R40_7427015_100MHz_insertion_loss.png"
    caption="Measured insertion loss (S21) of an 8 turn choke on TDK N30 R40, Amidon FT140-43 and Würth 7427015">}}

Please ignore the "dips" between 70 - 100MHz. They are most likely caused by resonances in my test setup. 

TDK's N30 material shines on frequencies up to 7 MHz. It still provides reasonable results up to 30MHz, but in the range from 10...30 MHz the Amidon 43 and Würth 4W620 outperform TDK's N30. 

## So what's the best material? (Summary)

As so often in life, the answer is: "it depends". Since the three ferrite cores are similarly priced (3,50€ - 4,50€), my suggestions are:
- If the interferences are mainly below 7 MHz - use TDK's N30
- If the interferences are mainly above 7 MHz - use Würth 4W620 or Amidon -43
- If you have to cover the whole short wave range with just a single core - use TDK N30
- If you want the best possible choke - use two cores in series. TDK N30 + Würth 4W620 or Amidon 43

If you have to remember one figure from this post it would be the following one:

{{< figure src="/img/2021/06/8_turns_ft140-42_N30R40_7427015_60MHz_insertion_loss.png"
    link="/img/2021/06/8_turns_ft140-42_N30R40_7427015_60MHz_insertion_loss.png"
    caption="Measured insertion loss (S21) of an 8 turn choke on TDK N30 R40, Amidon FT140-43 and Würth 7427015 (1-60MHz)">}}

I hope this comparison gave you some indications on how to pick the right ferrite material for your common mode choke. Please don't forget, there are many more manufactures with even more ferrite materials. In doubt, measure the insertion loss (and impedance) of the choke to gain certainty.
