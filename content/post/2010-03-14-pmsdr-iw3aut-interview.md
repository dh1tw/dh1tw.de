---
title: PMSDR – an interview with IW3AUT
author: Tobias (DH1TW)
layout: post
date: 2010-03-14T00:26:02+00:00
url: /pmsdr-iw3aut-interview
categories:
  - Software Defined Radio
tags:
  - kit
  - PMSDR
  - Software Defined Radio
thumbnailImage: "img/2010/03/pm_sdr.jpg"
thumbnailImagePosition: "left"

---
This week I had the pleasure to interview Martin, IW3AUT. He's the developer and founder of the Italian PMSDR Software Defined Radio receiver. In this interview you will get a look inside a successful SDR project. You will read about the design goals, the milestones of the project, the problems which Martin encountered an how he solved them. Enjoy the interview!
<!--more-->

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Hey Martin, I’m glad to be able to interview you today. You are the leading person behind the PMSDR, a Software Defined Radio kit, which entered the &#8220;arena&#8221; in 2009. Before we go into detail about the SDR you developed, I am keen to know how you found your way into Amateur Radio.</span></em>
</p>

<p style="text-align: justify;">
  <strong> </strong>
</p>

**IW3AUT:** My “radio career” started with the soft age of 11 when I had my first contact with CB-Radio. With the age of 16, I passed the Amateur Radio exam and received the callsign IW3AUT which I&#8217;m still holding today. I am an enthusiastic Short Wave- / Broadcast listener and I have a passion for microwave applications.

{{< figure src="/img/2010/03/iw3aut.jpg" link="/img/2010/03/iw3aut.jpg" >}}
_Martin, IW3AUT_

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Did your professional career have any influence on your Amateur Radio activities?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> Definitely! So far I worked already within the electronics, industrial electronics and  IT.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> How did you get interested in SDR?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> My first contact with Software defined Radio was during the annual <a href="http://www.i-link.it/convegno11.htm">i-Link Convention for Digital & Radio Communications</a> in Costalovara, northern Italy. From the beginning on I was amazed by the performance of such simple (speaking in terms of hardware design) receivers, described by the most famous SDR-Developers in Italy.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> What was your motivation to develop the PMSDR?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> Without any doubt, this technology is the future of radio technology. This technology is the enabler to build better and less expensive radio devices, although the main development effort is shifting now from the hardware into the software. This means that the quality of the software is influencing more and more the overall quality of the system.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Where do you see the advantages & disadvantages of SDR by today?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> As already mentioned, the development effort is concentrating more and more on the software. However, and this might be the disadvantage, the development of such devices / software require a good knowledge of digital signal processing (DSP).<br /> But thanks to the ongoing industrial developments and steady decreasing prices of semiconductors (especially the Analog/Digital Converters (ADCs) and FPGAs), the Software Defined Radio will replace the “conventional” radios within the near future.<br /> With an SDR it’s not only possible to hear, we are also able to see what we hear.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Could you describe in a few words the concept of the PMSDR?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> The PMSDR is a small, low-cost, HF bands full coverage Software Defined Radio receiver. PMSDR is controlled and supplied exclusively through the USB port and it delivers the I-Q audio signals to the PC&#8217;s sound card.<br /> The PMSDR is based on a Quadrature Sampling Detector (QSD), similar to the Softrock project, but with much more features. The PMSDR is using an onboard Microcontroller to control the various parameters like operating frequency or the bandpass filter settings via USB.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Why did you choose the QSD concept and not a Direct Sampler?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> I decided to go for a QSD because of its simplistic approach. When I took this fundamental design decision I also did not have the know-how to develop the software for a Direct Sampling receiver’s FPGA. I know, there are certain limits with a QSD which a Direct Sampling Receiver doesn’t have. But I think the low complexity of a QSD can also be seen as an advantage. It improves the rate of successful builds and lowers the rate of assembling / design aborts.
</p>

<p style="text-align: justify;">
  Direct Sampling is definitely the technology you want to bet on in Software Defined Radio. In my future development projects I will seriously consider to switch to the direct sampling concept.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Did you develop the PMSDR from the beginning with the intention to make it available for other Hams?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> No, in the beginning I developed the PMSDR for personal use only. However after receiving a lot of requests, I created a kit and added a proper enclosure. The kit itself consists of a professional manufactured PCB with 175 pre-mounted SMD parts. Only a few more (non-SMD) parts have to be added. The kit does not require special solder experience.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Which is the target group you address with the PMSDR?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> Mainly Shortwave listener, Broadcast listener and licensed OMs
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> What were the design goals of this SDR kit?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> I had five major design goals:
</p>

<ol style="text-align: justify;">
  <li>
    Low cost
  </li>
  <li>
    Low power consumption (less than 200mA) with the possibility to be supplied through the computers USB connection
  </li>
  <li>
    Coverage from 100kHz…55MHz
  </li>
  <li>
    Compatibility to various SDR software (Winrad, PowerSDR, G8JCFSDR, etc.)
  </li>
  <li>
    A kit – because we all like to solder
  </li>
</ol>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Why did you choose to use the Si570 programmable crystal oscillator and not a Digital Direct Synthesizer (DDS) for clock generation?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> The Si570 is of the few programmable clock generators which come with a very low phase noise. In most cases the phase noise is much lower than the phase noise of PLL’s used in our “standard” transceivers.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> What design tools did you use?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> I designed the schematic and PCB in <a href="http://www.cadsoft.de/">Cadsoft’s Eagle</a>. For RF-Simulations (e.g. filter design) I used RFSim99.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> How long did it take to develop the PMSDR?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT: </strong>I started with the development in 2007 and it took me about one year of continuous work in the evenings and on the weekends. The first prototype used a PLL clock generator (Cypress CY2293x). Due to the high phase noise I decided to replace it with a SiLab Si570 on the second prototype. It took me about  another two months to incorporate the changes until I had the second prototype in my hands. However the biggest chunk of work was writing the firmware and the DLL software library. Apart from the software & hardware developments another huge time consumer is the creation of the PMSDR documentation and keeping the webpage up to date.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> What kind of problems did you encounter during the development?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> The most challenging problems I had were the suppression of unwanted signals emitted by the voltage supply (the computer) and writing a flexible software interface for Winrad.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> How did you solve these problems?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> Through design changes in the circuits. One of my lessons-learnt was the importance of having proper decoupled supply voltages for the ICs. Especially for those where fast logic meet analog signals. Additionally the importance of impedance matching between mixer and IF-mixer is also often underestimated.
</p>

<p style="text-align: justify;">
  I was not a very active OM and for a developer the real user needs are not always obvious. After rolling out the first batch of PMSDRs I received more and more suggestions and wishes from active Hams. This is one of the reasons why I finally dedicated much more time on the software (firmware / DLL) development as earlier estimated.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Do you have any recommendations for the readers who want to develop a SDR receiver or transceiver by their own?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> In any case, make sure you understand the theory of digital signal processing. DSP theory is the foundation of SDR development.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> As heard earlier, the PMSDR is a QSD, similar to the softrock sdr kit which was developed by Tony Parks, KB9YIG. Could you sum up the differences between the PMSDR and the Softrock kit?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> The most obvious differences are that PMSDR:
</p>

<ol style="text-align: justify;">
  <li>
    is tuneable from 100kHz … 55MHz
  </li>
  <li>
    has a switchable stack of bandfilters and provides an interface for a LCD
  </li>
  <li>
    is shipped as a pre-assembled SMD-kit
  </li>
  <li>
    is supported by a comprehensive DLL Software library which provides a CAT transceiver interface and station database interface
  </li>
  <li>
    is a single PCB SDR
  </li>
  <li>
    supports an arbitrary start frequency, defined by the user
  </li>
</ol>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> So why should my readers consider buying a PMSDR kit?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> The PMSDR is an interesting product for everyone who needs a flexible, expandable SDR receiver with full shortwave coverage for a reasonable price.
</p>

<p style="text-align: justify;">
  The PMSDR can be operated in various configurations. Thanks to it’s switching options, it might be used in parallel with a transceiver on the same antenna or as a PanAdapter in the receivers IF-Output of a Transceiver. The PMSDR can be controlled from various Operating Systems, including Linux. The availability of the comprehensive software DLL library provides a flexible control interface for the radio which can be included in various SDR software packages. This is an important fact, since the buyers will increasingly consider the amount of software features in their future SDR purchases.
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> What is the roadmap of the PMSDR? Have you already planned any improvements or add-ons?</span></em>
</p>

<p style="text-align: justify;">
  <strong>IW3AUT:</strong> By today, two add-ons are already available for purchase, the antenna switching Board and a galvanic antenna isolation kit. Within 2010 VHF / UHF down-converters and an optional preselector should become available for the PMSDR. In the long term future I’m would like to develop a new SDR receiver / transceiver. We’ll see…
</p>

<p style="text-align: justify;">
  <em><span style="color: #3366ff;"><strong>DH1TW:</strong> Martin, thank you very much for this interesting interview! I would also like to thank you for the development of the PMSDR. Folks like you are moving Amateur Radio with big steps into a new era!</span></em>
</p>

<p style="text-align: justify;">
  <br class="spacer_" />
</p>

<p style="text-align: justify;">
  <strong>Shownotes:</strong>
</p>

<ul style="text-align: justify;">
  <li>
    <a href="http://www.iw3aut.altervista.org/">PMSDR Website</a>
  </li>
  <li>
    <a href="http://www.rfsystem.it/shop/">RF System Webshop</a>
  </li>
</ul>