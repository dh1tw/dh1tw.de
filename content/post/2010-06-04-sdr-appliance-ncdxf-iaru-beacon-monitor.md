---
title: 'SDR appliance: JN1SDD’s NCDXF / IARU Beacon Monitor'
author: Tobias (DH1TW)
layout: post
date: 2010-06-04T05:00:24+00:00
url: /sdr-appliance-ncdxf-iaru-beacon-monitor
categories:
  - DSP
  - Software Defined Radio
tags:
  - Faros
  - NCDXF / IARU Beacon Network
  - Software Defined Radio
thumbnailImage: "img/2010/06/lighthouse.jpg"
thumbnailImagePosition: "left"


---
On my ongoing search for SDR appliances, I discovered a couple of weeks ago an SDR (Softrock & Linux) based Beacon Monitoring System. The system is making use of the [NCDXF Internation Beacon Project (IBP)](http://www.ncdxf.org/beacons.html) which consists of 18 timely synchronized automated transmitters, located around the world. It monitors the signals on the various bands and generates in real-time a graphical chart showing the signal's strength. The chart is uploaded to a webserver and accessible for everyone through the Internet. Lately I had the possibility to interview the author of the system, Atsushi (JN1SDD). In this interview he revealed with great deepness how the system is build up. I hope you will enjoy this interview as much as I did!
<!--more-->
<br>
<div style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW:</strong> Atsushi, thank you so much for volunteering for this interview! Before we start with the technical details of your </span><a id="fsai" title="Beacon Monitoring System" href="http://www.ayoko.net/faros/"><span style="color: #3366ff;">Beacon Monitoring System</span></a><span style="color: #3366ff;">, I would like to know who is the person behind the callsign JN1SDD. What brought you to Ham Radio? What was your motivation to obtain a Amateur radio license? </span>
</div>

**JN1SDD:** My father was running a small electric factory when I was little, and there were so many electric parts and related books around me.  I naturally got interested in that area.  Especially in microcomputers.

Regarding amateur radio, I don't remember very much, but one day I found related articles in some specialized magazines. Honestly speaking, amateur radio was a secondary interest for me.  However, I also remember that I found a nice book, when I was an elementary school kid, which taught me that amateur radio was what an attractive hobby. I believe, I still might not have a license today if I haven't got this book into my finger.

I needed to study hard for university entrance exam, so I had to postpone the amateur radio license exam. but finally after entering the university, I obtained a license. At that time it was a 4th class license. (Currently I have much higher grade license though)

<span style="color: #3366ff;"><strong>DH1TW:</strong> For how many years are you holding now your Amateur radio license?</span>

<span style="font-family: arial, sans-serif;"><strong> </strong></span>

<p style="text-align: justify;">
  <strong> </strong>
</p>

{{< figure src="/img/2010/06/atsushi.jpg" link="/img/2010/06/atsushi.jpg" >}}

_Atsushi, JN1SDD_

**JN1SDD:** From license point of view, I&#8217;ve been licensed now for 21 years. But mainly I was a &#8220;listener&#8221; instead of an operator. I like to receive any radio but not good at operation, honestly speaking.

<div style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW:</strong> How did you find your way to Software Defined Radios?</span>
</div>

<p style="text-align: justify;">
  JN1SDD: When I joined the first company, my job was writing software for DSP (or digital signal processor). I was mainly working on speech signal processing, especially speech codec and audible signal detection for mobile phone handsets. I remember, when I heard the term &#8220;SDR&#8221; for the first time, I thought that it was just a configurable modulator and demodulator and related to FPGA although it contains the word &#8220;software&#8221; in the abbreviation. I guess, I thought any DSP of that time was not fast enough for such application. For me, SDR had some kind of breakthrough when I saw an introduction to SoftRock in a amateur radio magazine, a couple of years ago. However at that time I still had doubts that the SoftRock radio was more a kind of toy rather than something practical.
</p>

<div style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW: </strong>You mentioned, that you were developing DSP software. Do you still maintain this job?</span>
</div>

<p style="text-align: justify;">
  <strong>JN1SDD:</strong> Yes, at that time I was implementing speech codec for CDMA mobile phones. After working as an embedded software designer for 8 years, I moved to the current job, where I am a field application engineer at a semiconductor company. I&#8217;m involved in the software engineering of cellular phone base stations. I think my job isn&#8217;t that far from amateur radio since recent ham radio transceivers are also equipped with DSPs.
</p>

<div style="text-align: justify;">
  <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Let&#8217;s come to your beacon monitoring system. Could you give my readers a rough overview about the functionality and the key features of your Beacon Monitoring System?</span>
</div>

<p style="text-align: justify;">
  <strong>JN1SDD: </strong>My beacon monitor continuously listens to HF beacon signals which are allocated in the 14, 18, 21, 24 and 28 MHz bands for 24 hours 365 days. Current I&#8217;m using one physical receiver (a SoftRock kit) which changes between the five bands every 15 minutes. Each NCDXF beacon has a time slot of exactly 10 seconds which is repeated every three minutes. A beacon transmission consists of the individual callsign and four continuous carriers at 100 W, 10 W, 1 W and 0.1 W. My Beacon monitoring system checks the Signal to Noise ratio of the beacons and generates a comparison chart which is uploaded on my webserver.
</p>

<div style="text-align: justify;">
  My Beacon monitoring system is similar to Faros, and application written by Alex Shovkoplyas, VE3NEA. However I wrote the whole system from scratch by my own.
</div>

{{< figure src="http://www.ayoko.net/faros/png/today.png" link="http://www.ayoko.net/faros/png/today.png" >}}

_Real-Time Propagation Chart, generated by JN1SDD's Beacon Monitoring System_

<span style="color: #3366ff;"><strong>DH1TW: </strong>Knowing about Faros, what was your motivation to create a beacon monitoring system by your own? Why did you choose to develop your own application instead of using an already existing one?</span>

<p style="text-align: justify;">
  <strong>JN1SDD:</strong> Indeed, Faros is a great software, but I has just two dissatisfactions: First, its a Windows application and does not run on Linux. Second, Faros is a black-box &#8211; there is no way to see how it actually works. Let there be no misunderstanding, after developing my own beacon monitoring system I admit that writing such a software is a complex task and consumes a lot of time. I suppose that is the reason why the author of Faros does not treat it as a free software. Writing code, which determines if a received signal is considered a beacon or just noise, is a tough thing.
</p>

Anyway, I decided to build the beacon monitor by myself. I had two goals:

<ol style="text-align: justify;">
  <li>
    Use Linux as the operating system
  </li>
  <li>
    Implement my own ideas.
  </li>
</ol>

<div style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW:</strong> Why Linux instead of Microsoft Windows?</span>
</div>

<p style="text-align: justify;">
  JN1SDD: Linux is an operating system which does not need frequent interaction by human hand. Thanks to the great command line (tools), remote maintenance does not require a Graphical User Interface (GUI). For Linux, a lot of useful documentation is free available. Linux is inexpensive or free so I did not need to pay for a Windows license for the beacon monitoring system. With it&#8217;s reliability Linux is a great foundation to develop a system which shall be operated 24 hours a day, 365 days a year.
</p>

<p style="text-align: justify;">
  <span style="color: #3366ff;"><strong> DH1TW: </strong>Which Linux distribution are you using?</span>
</p>

<div style="text-align: justify;">
  <strong>JN1SDD:</strong> I&#8217;ve chosen Debian/GNU Linux.  I&#8217;m usually using NetBSD and therefor not very familiar with Linux.  I thought that Debian was straightforward from optional software package maintenance standpoint. I found that a lot of packages were available and well maintained. I also evaluated Ubuntu, but I did not choose it, because I had no need for the rich GUI interfaces. My beacon monitor does not require a GUI at all.  &#8220;Simpler systems are rarely broken&#8221; is my experience! 🙂
</div>

<span style="color: #3366ff;"><strong>DH1TW: </strong> When you started the development, did you had a clear idea from the first day on or did you elaborate the design over time?</span>

**JN1SDD:** I did not have a clear idea at the beginning, I tried to &#8220;progressively elaborate&#8221; the system. For instance, my original plan was to to use C language to implement the heart of system. But later, I changed to Octave. After designed a prototype, I also noticed that Bayesian statistic could be used to detect the beacon signals, so I implemented that.

<span style="color: #3366ff;"><strong>DH1TW: </strong>How long did the development of the overall system take?</span>

 **JN1SDD:** The total time was about 2 or 3 months. I worked for the project in lunch-breaks in the office and also in my free time the evenings.

<span style="color: #3366ff;"><strong>DH1TW: </strong>Could you describe briefly the functionality of each software module (Signal Recorder, Signal Archiver, Parameters Extractor, Bayes Classifier, Chart Drawer) and why you have chosen the corresponding programming language?</span>

{{< figure src="/img/2010/05/software.jpg" link="/img/2010/05/software.jpg" >}}

<div style="text-align: justify;">
  <p>
    <strong>JN1SDD:</strong> Ok, as mentioned, I wanted to write the code step by step, therefor I adopted a kind of modular design instead of monolithic one. As a basis of all, I needed to record the signals, so I wrote a signal recorder software prior to any other modules.
  </p>
</div>

{{< figure src="/img/2010/05/signal_recorder.jpg" link="/img/2010/05/signal_recorder.jpg" >}}

<div style="text-align: justify;">
  <p>
    The signal recorder is intended to record I/Q signal from SoftRock day and night without interruption.  To determine if a signal is transmitted by a beacon or not, accurate time information is also required. The signal recorder stores the raw signal and timing information into disk. Each of this data is stored in an individual file. Another reason why I wrote the Signal recorder first, was because I was unsure if Linux could actually allow me to implement near real-time software system. Recording the signals without interruption was a crucial success factor of the beacon monitoring system.
  </p>
</div>

{{< figure src="/img/2010/05/signal_archiver.jpg" link="/img/2010/05/signal_archiver.jpg" >}}

<p style="text-align: justify;">
Storing 48kHz sampling data requires a amout of hard disk space. One the one hand I want to archive the signals for a long time but on the other hand I have limited hard disk space. So I wrote the Signal Archiver which creates the absolute signal out the the I/Q stream and reduces the bandwidth to 2kHz. This shrinks the size to 1/48 of the original file size.
</p>

{{< figure src="/img/2010/05/parameter_extractor.jpg" link="/img/2010/05/parameter_extractor.jpg" >}}

<p style="text-align: justify;">
The next step is the parameter extraction for each 10 seconds signal block. The Parameter Extractor looks into received signal and calculates some characteristics of the received acoustic signal. These are the most important characteristics:
</p>

<div style="text-align: justify;">
  <ol>
    <li>
      S/N ratio between the peak signal in a specific band width compared to the estimated background noise.
    </li>
    <li>
      Frequency bias between the candidate peak signal and expected true frequency. To my best knowledge, oscillator of the some beacon station transmitters have a small frequency offset to the nominal frequency. It sometimes reaches 6 or 7 ppm compared to the nominal.
    </li>
    <li style="text-align: justify;">
      How long the candidate peak signal was continuously received. I also check that the signal was not received earlier or later than expected against an accurate time base.
    </li>
  </ol>
</div>

<div style="text-align: justify;">
  <p>
    There are some additional parameters, but this would go take much more time. For the saceness of completion I just want to mention that I currently do not decode the CW signal in any way.
  </p>
</div>

{{< figure src="/img/2010/05/bayes_classifier.jpg" link="/img/2010/05/bayes_classifier.jpg" >}}

<div style="text-align: justify;">
  This is the heart of beacon monitor.  It receives the above parameters and makes the judgment whether the signal is a beacon station or just noise. At <a id="ynhq" title="Wikipedia Bayes Classifier" href="http://en.wikipedia.org/wiki/Naive_Bayes_classifier">Wikipedia Bayes Classifier</a> are explained quite well. By the way, one tough thing is that Bayes classifier need to be trained by our ears. The classifier is not a magic wall or it does not outstrip the trainer.
</div>

{{< figure src="/img/2010/05/chart_drawer.jpg" link="/img/2010/05/chart_drawer.jpg" >}}

<p style="text-align: justify;">
  The Chart Drawer simply draws the charts and diagrams visualizing the monitoring results which are then uploaded to the internet. The charts are similar to VE3NEA's Faros charts. It also generates a chart on an azimuthal equidistant projection of the earth where my beacon monitor station is located at the center of the map.  It shows day and night area of the earth surface to help audience to have better understanding of the radio propagation.
</p>

<p style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW: </strong>In the Software System Diagram I can see that you use a variety of Software languages and tools. Why did you choose C, Octave, AWK and Python? Why not just a single programming language?</span>
</p>

<p style="text-align: justify;">
  <strong>JN1SDD: </strong>Thank you for asking 🙂  I know that many engineers rely on a single programming language. Going a little bit off-topic &#8211; I remember some coworkers of mine use Microsoft PowerPoint not only for presentation but also for word processing or just email attachment. Anyway, I like the right language for the right job instead.
</p>

<div style="text-align: justify;">
  My most favorite languages are AWK and Bourne shell. They are both well known in Unix-like operating system community. They are well designed and also matured. Especially, AWK has very simple syntax and well controlled not to be extended so often, but is still powerful for text processing and also simple numerical calculation.
</div>

<p style="text-align: justify;">
  On the other hand, recent programming languages such as Python, are much more flexible and powerful. However I feel they are somewhat more complicated for do-it-yourself programmers because we need to memorize so much syntax and convention.  I usually try to write any programs, especially for prototypes, in AWK or Bourne shell as much as possible.<br /> I also used Octave because I found it was quite useful for signal processing programming.  It handles vectors and matrices in a very handy way. Some essential and utility functions are ready to use, for example, digital filter and FFT.  Octave code can be put in a text file, so it can be executed easily and similar to a shell script. This makes it easy to collaborate with other languages or tools. It adopts common Unix OS manners well, I think.<br /> However, I was very new to Octave, so I often puzzled over to realize what I wanted to do.  In theory, we can use Octave like any other generic language, but as you know, signal processing often requires iterative calculation. Therefore, I had to iterate the performance by improving the code through many design loops.  After a while, I noticed that a better understanding of Octave helped to obtain better performance and smaller code. Bad  performance by Octave was often caused by wrong usage of it.<br /> By this experience, now I got confidence that any fresh DSP engineer or enthusiastic Ham should put Octave (or MATLAB) to practical use whenever they try their own algorithm for signal processing or control.  Recent microcomputer or DSP require much higher skills than past to gain the optimized performance, due to its deeper pipeline structure and VLIW.  I think that Octave will give new engineers good insight to gain optimized performance also for industrial-level implementation by DSP or FPGA.
</p>

<p style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW: </strong>How did you realize the interfaces between the programming languages?</span>
</p>

<div style="text-align: justify;">
  <strong>JN1SDD: </strong>I didn&#8217;t consider that I needed any special database format. I simply cut I/Q signal in multiple files on a daily basis.  Other files are just stored in simple text format.  All lines are separated by spaces because AWK programming language is suitable to handle that. However I saw a pitfall when I was writing a cleaning script. The script periodically removes outdated I/Q signal files due to the large sizes. When removing the 16 GB file which corresponds to one day reception, Linux file system seems to suffer a severe performance degradation. In the result, the signal recorder process often misses the real-time deadline. I needed a small invention to avoid the problem.
</div>

<p style="text-align: justify;">
  <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Do you have for comparison any experience with soundcard handling under Windows?</span>
</p>

<div style="text-align: justify;">
  <strong>JN1SDD:</strong> No, I don&#8217;t.  Only exception is I had experience using Playrec for Octave.  It realizes to implement near real-time signal processing for audio bandwidth by microphone or speaker.  I&#8217;ve ever adopted Playrec when I needed to write a small script for a transceiver adjustment.
</div>

<p style="text-align: justify;">
  <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Now, after having finished the developed, what was the most difficult part?</span>
</p>

<div style="text-align: justify;">
  <div>
    <strong>JN1SDD:</strong> I remember two major difficulties: The first one was realizing a real-time response by Linux. I still see a small chance that the software misses a deadline on I/Q signal reception at sound card. I guess I need to make me more familiar with ALSA driver requirement.
  </div>

  <p>
    The second challange was how to tell the Bayesian classifier which signals belong to beacons and which did not.  I needed to listen to recorded signals for more several hours. This was an exhausting work, because most of the signals were just noise. I had to listen to so carefully to hear the weak beacons, so it often made my heart skip a beat 😉
  </p>

  <p>
    <strong><span style="color: #3366ff;">DH1TW: </span></strong><span style="color: #3366ff;">If you would develop a Beacon Monitoring System again, is there anything which you would do different today?</span>
  </p>

  <p>
    JN1SDD: From implementation point of view, I want to draw a clear blueprint prior to implementation.  In my code, there are currently still many disjointed naming conventions of software block parts and variables. Maybe I might split the software system into a real-time sensitive part and a non-real-time part. The former needs to be ran on a physically dependent PC but latter may be ran on a virtual machine on VMware server or physically remote system. It may reduce power consumption which would be better for earth&#8217;s environment.
  </p>

  <p>
    <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Are there any plans to make the source code available for other hams?</span>
  </p>

  <p>
    <strong>JN1SDD:</strong> Yes, there are! However, I have not tested the monitoring system in another PC enviornment than my own. Other hardware may require  modifications to the software. Especially the current signal classifier was tested only in my environment. I&#8217;m not sure if it has to be readjusted in other environments. Additionally, I will have to clean up the source code so that anybody can read it.
  </p>

  <p>
    <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Do you have further plans to extend and / or enhance the beacon monitoring system?</span>
  </p>

  <div>
    <strong>JN1SDD:</strong> An idea is to have multiple antennas and receivers in order to shorten the reception interval of beacons on multiple frequency bands. For instance, the current system can not receive beacons which are transmitting on 18 MHz while listening at the same time to beacons on 14 MHz.
  </div>
</div>

<div style="text-align: justify;">
  I have ideas about an automatic calibration of SoftRock local oscillator. My beacon monitor depends on accurate frequency of the local oscillator to determine if a signal is of a beacon or not. The accurate calibration would also help me to provide frequency deviation values of the beacon stations to other beacon monitor stations by Internet. It might help them to determine if the signal came from an actual beacon station or not, especially when the signal was quite weak for receiving stations. In fact, I can easily monitor VR2B but not for CS3B.
</div>

<p style="text-align: justify;">
  <strong><span style="color: #3366ff;">DH1TW: </span></strong><span style="color: #3366ff;">By today, many Hams are curious about Software Defined Radio and their appliances. By today there are several inexpensive kits and rich feature software packages available. They somewhat paved the way as an entrance into the world how Software Defined Radio. But since Ham Radio was always about experimenting I can see that a lot of my friends find it difficult to find the transition from the soldering iron into a  Software Development Environment. What is your suggestion to our fellow Hams who are enthusiastic in discovering and creating their own SDR appliance, but don&#8217;t know where to start?</span>
</p>

<p style="text-align: justify;">
  <strong>JN1SDD: </strong>I&#8217;m also very new to SDR, so I don&#8217;t have enough confidence, but I recommend some inexpensive kits first. If we experience fully-packaged SDR from the beginning, we may be hard to find difference between traditional &#8220;soldering-iron&#8221; radio and SDR. They will say &#8220;It&#8217;s a commercial grade SDR. It is very natural that it has similar performance compared to the traditional off-the shelf transceiver.&#8221;
</p>

<p style="text-align: justify;">
  In fact, it&#8217;s still hard to believe that such tiny SoftRock receiver can receive beacon signals from LU4AA halfway around the world with my small antenna.<br /> On the other hand, I also understand very much that skilled radio amateurs still place complete trust in traditional off-the-shelf radio equipments. When we looked inside famous transceivers in the mid-1980s, there were so many electronics parts and cabling in the box.  I feel some uneasiness when we looked the hardware of SDR because it&#8217;s quite light for its size.<br /> However, recent transceivers from Yaesu or Kenwood are also equipped with DSP or digital signal processors.  I guess we will notice in the near future, any off-the-shelf transceivers became SDR, without realizing.<br /> In fact, recent infrastructure-grade communication equipments comprise a pair of high-speed ADC (analog digital converter), DAC (digital analog converter) and DSP.  This is certainly true around me although there were still important RF and IF analog devices in the equipments. I&#8217;m now seriously thinking that if I can build some amateur equipments by such electronic devices, for example, arbitrary waveform signal generator or spectrum analyzer, although I need much assistance of coworkers because I have less skill of RF hardware design.
</p>

<p style="text-align: justify;">
  <span style="color: #3366ff;"><strong>DH1TW: </strong>What are your plans for the future? Do you have already new (SDR) projects in mind?</span>
</p>

<p style="text-align: justify;">
  <strong>JN1SDD:</strong> Currently I&#8217;m preparing to take an exam for a professional radio license, so I have limited time to play around.  The license is not for job opportunity, but just to satisfy my curiosity.  After that, I will be back to SDR.  One plain is to improve the current monitoring station. I definitely want to add the automatic LO (local oscillator) calibration functionality. I also want to improve the appearance of my web site. Another plan is to build an SDR based LF receiver.  I&#8217;m very interested in the reception of 40 kHz low frequency time signal radio station (JJY).
</p>

<p style="text-align: justify;">
  As mentioned earlier, I also want to build some measurement equipments by industrial grade ADC or DAC, together with technology of SDR and FPGA.  I&#8217;m very curious about also for astronomy, photography and also biking, so I&#8217;m not sure when I can finally realize all the stuff I&#8217;ve mentioned 😉
</p>

<p style="text-align: justify;">
  <strong><span style="color: #3366ff;">DH1TW:</span></strong><span style="color: #3366ff;"> Awesome! I would like to thank you very much for this interesting interview. Thank you for sharing your experience and knowledge with us! I wish you a lot of success for your upcoming exam and I hope we&#8217;ll stay in touch.</span>
</p>

<h2 style="text-align: justify;">
  Shownotes:
</h2>

<div style="text-align: justify;">
  &#8211; <a id="yj3f" title="JN1SDD Beacon Monitoring System" href="http://www.ayoko.net/faros/">JN1SDD Beacon Monitoring System</a>
</div>

<div style="text-align: justify;">
  <a href="http://www.ayoko.net/faros/"></a>&#8211; <a id="mi.f" title="NCDXF International Beacon Project" href="http://www.ncdxf.org/beacons.html">NCDXF International Beacon Project</a>
</div>

<div style="text-align: justify;">
  &#8211; <a id="mpab" title="VE3NEA's Faros" href="http://www.dxatlas.com/Faros/">VE3NEA&#8217;s Faros</a>
</div>