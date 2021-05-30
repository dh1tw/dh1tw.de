---
title: "Troubleshooting Icom RS-BA1 network issues"
author: Tobias (DH1TW)
date: 2021-05-30T12:00:00+02:00
layout: post
categories:
  - Software
  - remote
  - it-articles
tags:
  - icom
  - rs-ba1
  - remote
  - windows
  - networking
thumbnailImage: "img/2021/05/rsba1_teaser.jpg"
thumbnailImagePosition: "bottom"
---

To access [Icom](https://www.icomeurope.com/en/) Radio remotely (over the internet), Icom sells the [RS-BA1 software](https://www.icomamerica.com/en/products/amateur/hf/rsba1/default.aspx). During the setup, I stumbled over a few, mainly networking-related problems. In this post, I describe the symptoms, the tools I used for network debugging (on Windows), and the possible solutions.

<!--more-->

## RS-BA1 Description

RS-BA1 is a pretty barebone software. It gets the essential job done to control your radio(s) remotely - however it lacks interfaces that are needed for the integration with 3rd Party software (like Logging or Digital Mode programs). There are some 3rd party alternatives available like [VA2FSQ's Win4Icom Suite](https://icom.va2fsq.com/), but they couldn't convince me so far.
It is also worth noting, that RS-BA1 exists actually in two versions v1 and v2. Both are sold as separate products. v1 (the latest version is 1.96) is most likely discontinued since this release dates back to 2018. As far as I can see, the main difference is that newer radios like the [IC-9700](https://www.icomeurope.com/en/product/ic-9700/) and [IC-7610](https://www.icomeurope.com/en/product/ic-7610/) with Dual VFO capabilities are only available in RS-BA1 v2. So if you are planning to buy the RS-BA1 software, make sure you buy version 2.

Icom's RS-BA1 consists of two Windows programs - 

1. Icom Remote Utility 
2. RS-BA1 Remote Control

The *Remote Utility* basically takes care of all the networking and radio setup. *RS-BA1 Remote Control* is the User Interface through which you interact with the radio.

{{< figure src="/img/2021/05/rsba1_remote_utility.jpg"
    link="/img/2021/05/rsba1_remote_utility.jpg"
    caption="A Screenshot of the RS-BA1 Remote Utility software">}}

{{< figure src="/img/2021/05/rsba1_remote_control.jpg"
    link="/img/2021/05/rsba1_remote_control.jpg"
    caption="A Screenshot of the RS-BA1 Remote Control software">}}

The *Remote Utility* implements the server and client-side at the same time. This is confusing, especially when you are trying to debug your setup. As you will read at the end of this post, the *Remote Utility* mixes parameters and makes implicit assumptions that are not documented. For remote access, RS-BA1 *Remote Utility* uses 3 UDP connections. By default, it will use the ports 

1. 50001 (Control)
2. 50002 (CAT)
3. 50003 (Audio)

## My Setup

Since RS-BA1 only runs under Windows, I opted for a Mini-PC with an Intel Gemini Lake CPU. After two years, I still believe that these Gemini Lake Mini-PCs are an excellent choice for this use case. They are fast enough, optimized for low power consumption, come with a Windows10 license, and are affordable (~200USD). I use a Beelink X45 and a Beelink GK55. At the radio station, an Icom IC-7300 is connected via USB to the Mini-PC.

## Adjust your firewall rules

To access the IC-7300 via RS-BA1, you have to open on the server-side (where the radio is located) the three UDP ports in your firewall and forward them to the PC on which you are running RS-BA1. On the client side, you don't have to open any port since the RS-BA1 client will always initiate the connection. As long as you are not on a corporate network, outbound connections are typically always allowed.

## Connecting to the remote PC

The radio is located at our radio station in Spain, but these days I'm living in Germany. Therefore I have to do almost everything remotely. Fortunately, plenty of good Remote Desktop solutions are available. For a long time, I used Teamviewer, but lately, it became very annoying. Teamviewer is supposed to be free for personal usage, but in my case, they falsely "detected" commercial usage twice already. With this, all connections to remote Computers time out after 60 seconds. You can open a support ticket, but it takes several weeks until they review your case and eventually put you on the free plan again.
A solid alternative to Teamviewer is [Anydesk](https://anydesk.com/en), and that's what I'm using currently for connecting to remote Windows machines.

## Connection failed

After installing RS-BA1 v2 on the Mini-PC located at the radio station, I was quickly able to set up everything and verify, that I can connect locally to the radio. So far - so good.

However, I was just unable to connect from any PC remotely. After a few seconds, the *Icom Remote Utility* showed the error **Connection Failed**.

{{< figure src="/img/2021/05/rsba1_connection_failed.jpg"
    link="/img/2021/05/rsba1_connection_failed.jpg"
    caption="Screenshot with the error message from icom rs-ba1 showing 'connection failed'">}}

I verified that the firewall rules in the router were correctly implemented and that the *Icom Remote Utility* was allowed to open network sockets in the Defender (Windows 10's built-in Firewall). Even after some trial & error, using a different client computer, I wasn't able to connect to the remote radio. This particularly baffled me, because in the past I never encountered this particular problem with the Icom RS-BA1 software.

## Inspecting the sockets
 
After a while, I remembered, that the great `netstat` (network + statistics) tool, has been ported and added to Windows. Since I couldn't obtain in the GUI any further hint, it was time to fire up the shell. 

The command `netstat -aon` will list all active connections / open ports on your system:

```text

PS C:\WINDOWS\system32> netstat -aon

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       8
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:808            0.0.0.0:0              LISTENING       3696
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING       2272
  TCP    0.0.0.0:5357           0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:7070           0.0.0.0:0              LISTENING       3708
  [....]

```

Since the list is pretty extensive we can pipe the output into `findStr` for string filtering.

```text

PS C:\WINDOWS\system32> netstat -aon | findStr "50001"
  UDP    0.0.0.0:50001          *:*                                    3708

```

So far so good, an application with the ProcessID (PID) of 3708 is listening on all network interfaces (`0.0.0.0`) on port `50001`. That's gonna be the *RS-BA1 Remote Utility*... or isn't it? 

To find the application with the PID 3708, we could look it up in the Windows Task Manager or just use the command `tasklist`, filtering for `pid` 3708.

```text

PS C:\WINDOWS\system32> tasklist /fi "pid eq 3708"

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
AnyDesk.exe                   3708 Services                   0     21,328 K

```

Woho! What a surprise! Instead of the expected *RS-BA1 Remote Utility*, **Anydesk** is using port 50001. After checking the [Anydesk documentation](https://support.anydesk.com/Firewall) it turns out, that **Anydesk is using the same port range (50001-50003) as Icom's RS-BA1 Remote Utility**. Anydesk uses these ports for the discovery of other instances in the local network via UDP/broadcast. 

To de-conflict the UDP ports, we could either change Anydesk through its [custom advanced options](https://support.anydesk.com/Custom_Client_Advanced_Options) or just use different ports in the *RS-BA1 Remote Utility*.

### Modern alternatives to netstat

On a side note, I found out that Powershell can also return us the same information in a one-liner: 

```powershell

PS C:\WINDOWS\system32> Get-Process -Id (Get-NetUDPEndpoint -LocalPort 50001).OwningProcess

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    354      23    19952      21176       7.63   3708   0 AnyDesk

```

And as always, the great [SysInternals](https://docs.microsoft.com/en-us/sysinternals/) also have a matching GUI tool called [TCPView](https://docs.microsoft.com/de-de/sysinternals/downloads/tcpview).

## Using Non-Default Ports in Remote Utility

I decided to use non-default UDP ports in *Icom's Remote Utility*. Instead of using the UDP ports 50001, 50002, and 50003 **I decided to use 40001, 40002, and 40003 instead**. I had also to update the firewall rules in the router accordingly.

Technically you could still listen on your internet-facing router on ports 50001-50003 and then forward the traffic to the ports 40001-40003 on the PC where the radio is connected to. That works for the Control Connection (50001 / 40001) since you can specify the port on the client side explicitly in the corresponding *server properties*.

{{< figure src="/img/2021/05/rsba1_server_settings.jpg"
    link="/img/2021/05/rsba1_server_settings.jpg"
    caption="A Screenshot showing the available parameters for a RSBA1 server">}}

However, when trying to connect to the actual remote radio, *Remote Utility* will return **Virtual serial device error.**

{{< figure src="/img/2021/05/rsba1_virtual_serial_device_error.jpg"
    link="/img/2021/05/rsba1_virtual_serial_device_error.jpg"
    caption="A Screenshot showing the text of the rs-ba1 error message 'Virtual serial device error.'">}}

Turns out, the software developer of RS-BA1 took the shortcut by not asking for the **cat** and **audio** UDP ports, but instead using for audio the port settings from the actual server (which is 40002 and 40003 in our case). That's inconsistent and wrong.

## Summary

Both, Icom's RS-BA1 and Anydesk use the same UDP ports (50001-50003). Either you change the settings of Anydesk or just use different ports (e.g. 40001-40003) for RS-BA1. You must use consistently the same port range because the RS-BA1 client will only send cat and audio on the ports specified on the server-side.  