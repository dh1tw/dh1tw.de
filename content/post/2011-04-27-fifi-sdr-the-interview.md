---
title: FiFi SDR – The Interview
author: Tobias (DH1TW)
layout: post
date: 2011-04-27T14:59:50+00:00
url: /fifi-sdr-the-interview
categories:
  - My Podcast
  - Software Defined Radio
tags:
  - FiFi-SDR
  - Funkamateur
  - My Podcast
  - Software Defined Radio
thumbnailImage: "img/2011/04/IGP6608.jpg"
thumbnailImagePosition: "left"

---
The FiFi SDR is a second generation allband HF receiver. Beside it's QSD it comes with a onboard soundcard and a powerful ARM Cortex M-3 CPU which leaves a lot of room for experiments. I was glad to win Kai-Uwe, DF3DCB one of the FiFi-SDR founders for an interview.
<!--more-->

# A system view on the FiFi SDR

{{< figure src="/img/2011/04/fifi-sdr-schematic.jpg" link="/img/2011/04/fifi-sdr-schematic.jpg" >}}

# Pictures of my FiFi SDR receiver

{{< figure src="/img/2011/04/IGP6607.jpg" link="/img/2011/04/IGP6607.jpg" >}}

{{< figure src="/img/2011/04/IGP6609.jpg" link="/img/2011/04/IGP6609.jpg" >}}

{{< figure src="/img/2011/04/IGP6615.jpg" link="/img/2011/04/IGP6615.jpg" >}}

# Shownotes

The authors of the FiFi SDRs are:

  1. Kai-Uwe Pieper, [DF3DCB][1]
  2. Günter Schweppe, [DK5DN][2]
  3. Matti Reifenrath, [DC1DMR][3]
  4. Rolf Meeser, DF9DQ
  5. Felix Erckenbrecht, DG1YFE
  6. Sascha Schade, DL1DRS

More links:

  * The FiFi SDR website is located at: http://tinyurl.com/fifisdr
  * For on the fly translation within your webbrowser - check out [Google Chrome][5]
  * An [interesting][6] which was published in Funkamateur magazine
  * The FiFi SDR group is using [TRAC][7] as their online collaboration platform
  * The project was created as an electronics project for the [Fichten-Fieldday][8]
  * The FiFi SDR can be purchased at the [Funkamateur website][9] Some impressions of the Fichten-Fieldday and the FiFi-SDR assembly

# Interview Transcription

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Hey everyone, this is Tobias, DH1TW, and I’m glad that I’ve got Kai-Uwe, DF3DCB for interview with me. Kai-Uwe was one of the makers of the FiFi SDR, or how we call it in German Fee Fee SDR. It’s a low-cost all-band SDR receiver, which is making use of today’s state-of-the-art technologies. It’s not only the SDR receiver itself which makes this project so interesting, also the circumstances under which it was developed are remarkable and should be an inspiration for us how young folks can be motivated in ham radio hardware and software development. So, Kai-Uwe, thanks for joining me today!</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Hello, Tobias, and first of all thank you for giving me an opportunity to introduce our project to your listeners!
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Great. So, I actually have now FiFi SDR right now in front of me, my buddy DK5TX was so kind and borrowed me his version. So, before we hear about the technical details, you did not develop the FiFi SDR alone, there was also a group involved. Could you explain a little bit, who was involved and how this took place?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s exactly right, Tobias, and it’s very important to say that I’m not the only developer. We were a team of six hams, and I was only responsible for the PCB layout, and the other 5 old men involved are: first, Matti, DC1DMR, he was our project manager and administrator for the online tools we used; then, Rolf, DF9DQ – he has written the firmware and was also involved in hardware design; Felix, DG1YFE, who specially designed the hardware of the RF front-end; Günter, DK5DN for hardware development, measurement and testing of the analog part; and Sascha, DL1DRS for the CPLD design. So, these 6 hams were involved.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Wow, that’s quite a group, sounds you guys took it really serious. What was the motivation for you guys to develop the FiFi SDR?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yeah, it’s quite funny, since 2005 our local chapter of the DARC organizes a fieldday for young people. Every year in June it is called Fichtenfieldday, short form is FiFi, it takes place near Attendorn, that’s about 70 kilometers East of Cologne. And we have about 80 participants every year. By the way, ‘Fichten’ in English are spruces, these trees that dominate the landscape here in the South of Westfalia. And one of the specialties of our event is that every year we present an electronics project of our own, that means that’s something that you cannot buy in a shop at the time. Every participant of our fieldday solders his own kit, his device, during the fieldday. The FiFi SDR was our 2010 project, it was introduced during the fieldday.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Ok, cool, so this means that the FiFi SDR during the fieldday was at least built up 50-80 times?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> That’s right, yes. We were successful about 50 times. And some of the participants decided to take it with them and solder it at home, but I guess 50 radios were finished on the fieldday, yeah.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> That’s amazing! So you guys develop every year for the fieldday and for the fieldday participants a new kind of electronics project. So let me dig a little bit deeper into that. Why did you actually choose to build that year an SDR receiver, did you have any experience yet, or how did you come up with that idea?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, I’ll just say that Günter DK5DN, one of our team members, is a professor at Fachhochschule Meschede University of Applied Sciences and in 2009 he attended a research project by one… by two of his students Michael Wiese and Winfred Rickert. They developed a very simple SDR receiver based on the Si570 Oscillator, and so we decided to revise the work and make it a suitable project for the 2010 FiFi.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Ok. So this means that you didn’t have to develop everything by yourself, you could use the work of those two students as a basis for your development which then ended in the FiFi SDR. What would you say are the key features of the FiFi SDR?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, well first it’s a low batch of receiver, of course. Covering the frequency range from long waves to short waves, but it’s very small in size, compared to… well, it’s comparable to the dimensions of one of those compact cameras that we have today.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> It’s like a cigarette box, isn’t it?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, right.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW: </strong>The same size as a cigarette box.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> And the control is compatible to the SoftRock40, so that most available PC tools can be used. And maybe one of the most interesting features is our integrated 96 kHz USB soundcard. It’s required because for notebook operation most of our up to date notebooks only provide a mono microphone input, but no stereo, and mono is not suitable for the IQ processing that this principle is based on. And the FiFi SDR is also powered via the USB, only a single wire connection between the FiFi SDR and a computer is needed. I guess that’s one of the main key features.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> I like that idea pretty much about having the USB, the soundcard already on board. I was doing experiments with SDRs for the last 3 or 4 years and, I don’t know, I owned now at least 5 or 6 external USB soundcards and I was never really happy with those external USB boxes, because whenever you wanted to go somewhere you had to take it with you, you had a lot of cables. So, I like pretty much that idea of having the USB soundcard directly on the device and not having the necessity to bring another box with you. So now you explained what the FiFi SDR is, what would you say is the FiFi SDR explicitly not?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Ok, first of all it’s not a transmitter, it’s only a software-defined receiver. And it was not intended to be a best-performance receiver, we only wanted to develop the best possible low-budget solution. We had to pay a lot of attention to the cost, because every guest of our Fichtenfieldday, for everybody the annual assembly kit is included in the price, in the participation fee.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Alright, that’s cool.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay. And in this case our project was only possible by some support funding of the DARC.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, I would like to talk a little bit more about that point. So all the participants get one of those kits every year for free, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s right.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> I don’t want to spoil another question, but I’ve seen that the FiFi SDR is also available as a kit now, if I understand it right, the DARC, they gave you some extra funds in order to make that happen, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, they give us some funding for every participant. It means that it’s not the project of FiFi SDR itself, but a part of the participation fee is funded by the DARC.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> That’s a well-spent one, I think.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, let’s come back to more technical issues. Maybe you could reveal some technical details regarding the RF part, maybe it’s a good idea to go quickly through the FiFi SDR design, like starting from the signal arrives from the antenna and until you hear it out of your speakers.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, okay. Well, our radio is… we decided to use a separate RF grounding, that means the first stage in the FiFi SDR is an RF transformer and it is followed by a preamp of a single JFET and then we have a phase reversal stage because we need the I/Q signals and we are using a transistor circuit for that.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Right.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, the FiFi SDR by the way uses the QSD principle, Quadrature Sampling Detector, that has also been used by some other project, as the local oscillator made by Silicon Labs Si570 Oscillator. Okay, something that’s maybe a little special is that we have this oscillator followed by CPLD, it’s a complex programmable object device, it has been programmed by Sascha. It is used for generating the switching signals with the 90-degree phase offset.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> And that’s all most of it, because the rest is standard circuitry, it’s well-known from other receivers. We use FET switch as a mixer, that’s followed by low-pass filter and low-noise operation amplifier.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so instead of using the old-school TTL or CMOS circuits you are using a CPLD to create the signal for the switching mixer, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, exactly.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> So I guess this makes you just more flexible in changing, for example, later on the divider ratio? For example.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s right.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> So maybe we tackle now a little bit more the physical layout, since you were the responsible person of designing the PCBs.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> How did you create the physical layout? How many PCBs did you have to make, how many PCBs did it finally involve, how many layers?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, it’s a very simple board, only one PCB with two layers only. A PCB has a size of approximately 5 by 8 centimeters. It has an optional socket for another PCB for pre-selector that we are developing at present. But the FiFi SDR itself has only one PCB. It only has 3 connectors. That’s, of course, 1 connector for the antenna, it’s a BNC, then we have the mini-USB socket for PC connection, and you only need one of these, it’s for powering, it’s for control and also for the USB soundcard, all in one cable. And if you want to use an external soundcard, we have a 3.5mm jack.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> So I can use both, I can use the onboard soundcard, but the FiFi SDR also provides the alternative to use an external or whatever soundcard.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, if somebody has a better soundcard, there are on the market soundcards with 192 kHz, it can also be used.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay. The kit itself, I can barely see any device which is not SMD. What was design decision, did you just go for the smallest size, or does it also have RF-related issues why you decided to build the kit almost completely on SMD?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, there are several reasons. First is… From the very first Fichtenfieldday we decided to use SMD because it is state-of-the-art, we wanted to prove that it is possible even for young people with not much experience to solder these parts. It’s very often heard that it’s not possible to do this as a hobby, but we wanted to prove the opposite. And second, we wanted to have very small device, and it’s also cheaper. It’s very difficult also to find all the parts that we need with this through hole technology.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Now speaking about the experience, when you’ve built up during last year’s Fichtenfieldday those 50 devices, did you encounter any problems with SMD or was it really that easy for everyone.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> No, no, of course, there are of course problems, because not everybody is so much experienced in that. And as you have seen if you have opened the radio, it is very small, so we had to provide some help. That was for example, that we soldered the microcontroller, this ARM7 by ourselves, we did that before the fieldday already. But with the help of some of our crew members and, of course, some devices like communication test set, and oscilloscope and signal generator, and parts like that, we were able to find all the bugs that people made, and we were lucky that we got them all running.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> The kit which you’re going to sell, will that include all SMD parts assembled on the PCB, or will everyone have to solder those PCB parts?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Ok, we’ll have to go into detail. We had some rests of parts that we didn’t solder on the Fichtenfieldday and we gave these parts away as complete kits, but these kits are no longer available now. That means we have no more rests, but there’s ready assembled version available now.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so and that’s ready-assembled, it includes everything, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Somebody who’s interested and says “Oh, I don’t have to solder iron” or “I just don’t feel comfortable soldering SMD” still can enjoy the FiFi SDR when he buys the ready-assembled version, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s right. It is available at, I may say that at Funkamateur magazine, because we are not a company, we don’t have any commercial interests, so we gave the complete project to this Box 73 company in Berlin and the version that they sell has all SMD parts populated, and you only have to solder the connectors, and a drilled housing kit also is included.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Sounds good. So, now speaking about the wrapping up the physical part, since you also, as we mentioned, we have an onboard soundcard, and we have that ARM processor on the FiFi SDR. Could you say some words about the embedded software which you had to write, maybe the main features?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, the software was made by Rolf. It provides the communication to this programmable oscillator and it also manages the automatic switching for optional filters, as we have this pre-selector will soon be available, and the first job of the software is to provide this USB soundcard. At present Rolf, DF9DQ, is also testing and providing a special branch of this firmware, he calls it FiFi SDR DSP, and this digital signal processing version is already able to provide SSB demodulation by itself. So the PC is only needed for choosing the frequency for audio output and as a power supply.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Oh, this sounds great, this sounds great… I think this is exactly the way we’re heading now with the general SDR development. Currently we’re still making use of the computer, but I believe that the computer is not that reliable, since and due to the nature of multi-tasking, I believe that in the future we will see more and more kits which will do the processing, all the digital signal processing directly in the hardware, and only maintain the non-real time critical aspects in the software, for example displaying waterfall diagram, and CW skimmer maybe. There’s no problem if the call sign is decoded a hundred milliseconds later or a hundred milliseconds sooner, but if I actually have to listen to an SSB signal and I have a lack of a hundred milliseconds, or I have breakouts about a few milliseconds, this really hurts. So I’m really curious, I haven’t seen that software version in the software in the SVN, so maybe after the interview you should give me the link and I’ll be curious to try that out.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yeah, alright, it is included, but it is only a branch, because it’s not the official version, but it is included. It is possible for you to test it.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, cool. So, having now described more or less the FiFi SDR, the product itself, I would like to tackle the project. How long did it take you guys to develop the FiFi SDR?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Well, as we have a new project every year, we do not have that much time. Based on the final stage of the student project that I mentioned, it took half a year. We started in the end of 2009 and the hardware had to be ready by May 2010 because our fieldday is in June, but that was the hardware, we are still providing the software, it’s still under change.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay. About half a year… What about the development process? As we heard earlier, you used the basis that came from the work at the university. And did you redesign it, did you do some simulations, how did you organize the testing? And in total, how much iteration did you need to finally come up with the design which has then been used for the fieldday, which I have in my fingers now?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, there was still a lot of work to do, because the student project was not originally made for producing 100 pieces offered, there was only a single PCB. In addition to the student version we had two additional prototypes, we called these the revisions 0.1 and 0.2.  And the 0.2 is already very close to the serial version that’s in your hands, that means it’s already fully functional. We found that a lot of changes had to be made compared to the university project, partly for performance reasons – for example, we replaced the AVR by a powerful ARM controller – and partly, it was simply a resign to costs, because the students used, for example, optocouplers to attenuate disturbances from the USB bus, whereas the FiFi SDR is simply built with separate voltage regulators for digital and analog part and a deliberate ground concept. And the RF front-end was also completely redesigned by Felix, DG1YFE, to avoid an expensive second transformer or two separate preamps for the I/Q signals. Felix decided to design a transistor, that’s phase reversal stages I mentioned before. And this analog stuff is quite tricky sometimes to prevent oscillating etc., but it’s fortunately this revision 0.2 was already okay, it met all our development objectives.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so if I understand it right, the main goal of the redesign was to increase performance and also to make it ready for a reasonable serial production, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, right, because we had to… we had to be cheap simply because of our idea to provide an assembly kit for everyone who is a participant at our Fichtenfieldday, so it’s a need, it’s not only nice to have.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> The kit is currently available from the publisher Funkamateur, what is the price?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> I think its 89 euro, yes, including housing.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> 120 US dollars, something like that. You’ve mentioned that you could save some money by eliminating, for example, the optocouplers from the PCB. How much did you actually save or what was the cost of one optocoupler, for example?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> I have not made all the calculation for the student project, but the optocouplers alone, there were, I guess, 8 of them inside it, because they were also included in the bus input, and in the bus output signals, no, in the switching signals, and there were some euros only for the optocouplers.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay. So it could be said that you reduced the price of 30 or 40 percent or so?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> At least.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> At least? Okay. Well, great. What kind of software tools did you use in order to enhance or further develop the FiFi SDR? Did you use MPLAB, or any CAD software, simulation software?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Well, not MPLAB, but designing the RF circuit we had some simulations to be made, we performed them in SPICE, in ADS and in RF Sim.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> RF Sim is freeware, isn’t it?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> I’m not very sure because I did not perform it by myself, but some of our members have access to professional software also in their companies. We are lucky to have these opportunities. And then for the digital part, for the ARM firmware Rolf used the GNU compiler and Sascha, DL1DRS, he made the CPLD, he used this ISE Design Suite 11…
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> …which is provided by the manufacturer?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, I think so; I’m also not sure about that. My part was the PCB and I simply used this tool Eagle, that should be well-known.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Do you guys live all close together or did you use any kind of collaboration tools?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s an interesting question, because it’s a very important aspect of our project, because 2 of the involved hams live in Munich, two of them are students in Aachen, and the other 2 live in South Westfalia, so we had to perform the complete development by means of online tools. We used web-based software project tool called Trac, which is hosted on Matti’s web server, and this tool includes a subversion system, a ticket system for all issues that come up during the development process and also a wiki, which is ideal for all the documentation stuff.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Having all the project information, project documentation online already, are you going to make the software source code and the schematics available as well?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Well, they are available. All parts of the project are open right from the beginning and anybody has access to the SVN repository, to the wiki and can also view the complete developments, discussions and so on in the ticket system.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> As far as I have browsed through the project’s website, I think we should know that most of the comments and most of the descriptions are written in German, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s right.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> But by today this shouldn’t be such a big problem anymore. We have a lot of good translation tools out. I’m personally using Google translation tools. They have two different kinds of translation tools – the one is the website where you go to and you post either URL or a text snippet and it will translate it for you, and the second option which I am using very frequently is included in Google’s Chrome browser. This means that you just go to a website like in Firefox or Internet Explorer and it will offer you automatically the translation of the whole website, so you don’t have to go to the other website, copy and paste the content, Google Chrome will actually translate the website instantly to you.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, right. That’s right, Tobias, and if somebody has further questions, it’s no problem to open a ticket and ask questions in English also.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> That’s great. Ok, so another question which I’m always curious is… what problems did you encounter during the development of the FiFi SDR, and how did you solve them?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, I guess this question would blow this interview, but I guess it’s still very interesting that everybody who’s interested in those details should visit our website, because as I mentioned all the development discussions can be read in the Trac system. And most of these tickets deal with hardware issues. I must admit I’m not quite aware of all the software issues, because those tricky solutions that Rolf had to find when writing his firmware, I don’t know, I’m referring to the USB card especially, that was quite an effort.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so you say that you documented all the conversations you had within the development community in your online collaboration tool. This means for my listeners, if one of them is interested to see how you actually solved, for example, the problem with the USB soundcard, that they can go to your website, and they can open this particular thread and they can see how you elaborated the solution from the beginning, from the actual problem report, then until you agreed on the final solution, right?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, you are right.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> I think this is quite a smart way, because I’m seeing this daily also in my work, that a lot of communication is happening through email, and this is almost a point-to-point communication, and even if you have some other colleagues, and you CC:, or you send them a blind copy, at the end of the day I think it is much better to have all this kind of development communication in such a web-based system that at a later stage if somebody leaves the project, somebody new joins the project, that he is able to assess what has already happened, what problems have already been encountered and not to start always from zero again. So I think it helps significantly.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, that’s right. We have not used it for the first time, but we have very good experiences especially with this FiFi SDR project now. And indeed, most people contacting us are using the system. That means there are only a few people who are writing emails, but a lot of people are opening new tickets and the advantage is that we do not have to forward the emails to anybody in the project, but we get an email notification once a new ticket is made and one who has best skills to answer the question is simply doing it.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> The device itself is available from the German publisher Funkamateur for only about 100 euro and that version is already assembled ready-to-go version of the FiFi SDR. You guys don’t sell any more of the kits, do you?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, it was too much effort for us and also for the Funkamateur company, because it is not that easy to solder it. It can be done if you have a team, the people who know the schematics, who are the developers and with the help of them it’s of course easy to solder it, but not for mass production, so it’s only available as a complete module now.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> And you already mentioned that you’re going to develop now a preselector. Could you tell us a little bit more about the future roadmap of the FiFi SDR, are you going to plan more add-ons?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, the preselector will be the project for our Fichtenfieldday 2011. The original board is only equipped with 30MHz low-pass filter, and I must say this is one of the main disadvantages of the FiFi SDR now. The preselector has been requested a lot of times and we promised to make it and it will be ready by June.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so what about the physical dimensions? Will we be able to install the band-pass filter within the FiFi SDR’s enclosure, or will this be another external box?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Yes, indeed, we’ll still fit into the box, it will be a second PCB of the same size placed on it and it will be a combination of seven low-pass filters and one high-pass filter which are automatically chosen depending on the reception frequency.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, so you’re also going to modify the firmware, that whenever another band is selected, the appropriate band-pass filter is also selected, right? So that I do not have to select it manually with an external switch or so, it will already be selected through the frequency and through the microcontroller.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> That’s correct. Yes, right. And you do not have to modify the housing, you have to unsolder this 30 MHz low-pass filter that’s on the radio. Some parts have to be removed, but the add-on PCB will be put on circuit, no wire connections are needed
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Sounds pretty much like Plug’n’Play.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Ha-ha, yes, it is.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Okay, let’s rev up the session. Where can my listeners find more information about the FiFi SDR?</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, I have made one of these small redirection links, because all information is available on our website and you can find it under the address <a href="http://tinyurl.com/fifisdr">http://tinyurl.com/fifisdr</a> .
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> So, Kai-Uwe, let me thank you for volunteering for this interview.</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> You are welcome.
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> I think you guys have done an amazing job not only in developing a powerful and affordable state-of-the-art SDR receiver, but also in the organization of your Fichtenfieldday. You know, for me it’s a true pleasure to see fellow hams like you or your group being so dedicated in bringing our beautiful hobby closer to young people. So again, let me encourage my listener to check out your website at tinyurl.com/fifisdr. So, nothing more to add from my side, thank you so much, Kai-Uwe!</span>
</p>

<p style="text-align: justify;">
  <strong>DF3DCB:</strong> Okay, thanks for your invitation and I wish you a lot of fun with the FiFi SDR!
</p>

<p style="text-align: justify;">
  <span style="color: #0000ff;"><strong>DH1TW:</strong> Thanks, see you!</span>
</p>

 [1]: http://df3dcb.sischa.net/album/albums.php
 [2]: http://qrz.com/db/dk5dn
 [3]: http://www.dc1dmr.de/
 [4]: http://o28.sischa.net/fifisdr/trac
 [5]: http://google.com/chrome
 [6]: http://www.df3dcb.de/FiFi-SDR_FA1110.pdf
 [7]: http://trac.edgewall.org/
 [8]: http://www.ov-lennestadt.de/fifi/
 [9]: http://www.box73.de/catalog/product_info.php?products_id=2313&osCsid=qirs6sre7pb1ndbb7e4k15geg1