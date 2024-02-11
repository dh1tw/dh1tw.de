---
title: "Protector for SKF ball-bearings on antenna masts"
author: Tobias (DH1TW)
date: 2024-02-11T12:00:00+02:00
layout: post
categories:
  - Hardware
  - 3D-printing
tags:
  - 3d-printing
  - ed1r
thumbnailImage: "img/2024/02/skf_ball_bearing_protector_teaser.jpg"
thumbnailImagePosition: "bottom"
---

At ED1R we use industrial ball bearings on our towers to turn the antennas. The ball bearings are reliable IF you protect them properly. We learned this lesson the hard way. After almost three years in service, I feel confident sharing our solution for adequately protecting the SKF bearings on antenna towers. 

<!--more-->

## Choosing industrial bearings

We have used [Yaesu GS-065](https://www.yaesu.com/downloadFile.cfm?FileID=972&FileCatID=155&FileName=GS%2D065.pdf&FileContentType=application%2Fpdf) ball bearings for almost ten years, which have served well and never failed. Unfortunately, they only support masts with diameters less than 65mm. From 2017 to 2018, we rebuilt our contest station and upgraded the steel masts to larger diameters (up to 76,2mm - 30 inches) with thicker walls. With the diameters well above 65mm we couldn't use the Yaesu bearings anymore. Luckily, SKF offers [rolling bearings in various diameters and shapes](https://www.skf.com/uk/products/mounted-bearings/ball-bearing-units/flanged-ball-bearing-units), of industrial quality, and at an affordable price. 

We installed on our towers [UCF-217](https://www.skf.com/ph/products/mounted-bearings/ball-bearing-units/flanged-ball-bearing-units/productid-UCF%20217), [UCF-216](https://www.skf.com/uk/products/mounted-bearings/ball-bearing-units/flanged-ball-bearing-units/productid-UCF%20216) and [UCF-213](https://www.skf.com/uk/products/mounted-bearings/ball-bearing-units/flanged-ball-bearing-units/productid-UCF%20213) ball-bearings.

{{< figure src="/img/2024/02/ucf217-just-after-comissioning.jpeg"
    link="/img/2024/02/ucf217-just-after-comissioning.jpeg"
    caption="SKF UCF217 bearing after installation on the tower">}}

{{< figure src="/img/2024/02/ucf217-after-comissioning-tower-top.jpeg"
    link="/img/2024/02/ucf217-after-comissioning-tower-top.jpeg"
    caption="SKF UCF217 bearing after installation on the tower">}}

## The problem

After one year, two masts didn't turn anymore. Visual inspection showed significant bird droppings and sand contamination from the nearby Sarah desert.

{{< figure src="/img/2024/02/contaminated-bearing.jpeg"
    link="/img/2024/02/contaminated-bearing.jpeg"
    caption="contaminated bearing">}}

After cleaning the bearings with several cans of brake cleaner, the antennas were finally moving again. But it was obvious that a more permanent solution was needed.

## The best solution

Ideally, you would consider the protection of your bearings before installation. A great example is the picture below from Peter, DJ7WW. Peter covered the bearing hermetically with a flexible rubber, similar to axle boots used in cars.

{{< figure src="/img/2024/02/bearing_protector_dj7ww.jpeg"
    link="/img/2024/02/bearing_protector_dj7ww.jpeg"
    caption="rubber boot protector installed by DJ7WW">}}

This rubber boot protector must be installed when the mast is introduced into the tower BEFORE antennas are attached.

## The second best solution

We needed a solution that could be added to the bearing with the mast and antennas already installed. I'm not a mechanical engineer, but luckily, my CAD skills improved since I started working with 3D printers. The design I came up with consists of two shells attached in the center to the mast. Both shells are pressed against together with M5 screws. An additional 3mm rubber string acts as a gasket, reducing water and dirt from leaking through the cracks.    

{{< figure src="/img/2024/02/skf_bearing_protector_3d_model.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_model.jpeg"
    caption="3D Model of the protector assembly (front view)">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_model_back.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_model_back.jpeg"
    caption="3D Model of the protector assembly (back view)">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_model_open.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_model_open.jpeg"
    caption="Half of the assembly">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_model_section_cut.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_model_section_cut.jpeg"
    caption="Section cut of the assembly with the SKF ball bearing">}}

## Production

After confirming the design by printing a scaled-down model, my 3D printers were busy for a few days. I designed the ball-bearing protectors so that each part would fit on a standard 220x220mm print bed. I decided to print the bearing protectors in [PETG](https://en.wikipedia.org/wiki/Polyethylene_terephthalate) over [PLA](https://en.wikipedia.org/wiki/Polylactic_acid) due to its higher temperature and better UV resistance. Today, I would probably print them in [ASA](https://www.cnckitchen.com/blog/comparing-pla-petg-amp-asa-feat-prusament). If I remember correctly, each part took around 20 hours of print time.

{{< figure src="/img/2024/02/skf_bearing_protector_on_3d_printer.jpeg"
    link="/img/2024/02/skf_bearing_protector_on_3d_printer.jpeg"
    caption="Printing one shell at a time on an Creality Ender5">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_printed_closed.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_printed_closed.jpeg"
    caption="3D printed bearing protector">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_printed_open_front.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_printed_open_front.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_printed_open_back.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_printed_open_back.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_printed_bottom.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_printed_bottom.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_3d_printed.jpeg"
    link="/img/2024/02/skf_bearing_protector_3d_printed.jpeg"
    caption="">}}

After printing, I sanded the parts and applied a layer of primer and multiple layers of white paint to increase the UV resistance further.

{{< figure src="/img/2024/02/skf_bearing_protector_painting.jpeg"
    link="/img/2024/02/skf_bearing_protector_painting.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_painted.jpeg"
    link="/img/2024/02/skf_bearing_protector_painted.jpeg"
    caption="">}}

## Installation

Back in Spain, we installed the ball-bearing protectors back in 2020.

{{< figure src="/img/2024/02/skf_bearing_protector_ready_for_installation.jpeg"
    link="/img/2024/02/skf_bearing_protector_ready_for_installation.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_installed.jpeg"
    link="/img/2024/02/skf_bearing_protector_installed.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_installed_2.jpeg"
    link="/img/2024/02/skf_bearing_protector_installed_2.jpeg"
    caption="">}}

{{< figure src="/img/2024/02/skf_bearing_protector_installed_3.jpeg"
    link="/img/2024/02/skf_bearing_protector_installed_3.jpeg"
    caption="">}}

## 3 Years later

3 years later, all masts are still turning smoothly. Last year, in 2023, we visually inspected the bearings and the protectors. We were pleased with the result. The bearing was clear of dirt, and the plastic of the protectors was still in good shape despite the hard UV exposure under the Spanish sun.

{{< figure src="/img/2024/02/skf_bearing_protector_2_years_later.jpeg"
    link="/img/2024/02/skf_bearing_protector_2_years_later.jpeg"
    caption="Visual inspection of the ball bearing protectors after 2 years">}}

{{< figure src="/img/2024/02/skf_bearing_protector_2_years_later_2.jpeg"
    link="/img/2024/02/skf_bearing_protector_2_years_later_2.jpeg"
    caption="">}}
