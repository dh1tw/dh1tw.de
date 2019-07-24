---
title: How to set up an Ubuntu Server on Amazon EC2
author: Tobias (DH1TW)
layout: post
date: 2012-05-07T13:43:59+00:00
url: /how-to-set-up-an-ubuntu-server-on-amazon-ec2
categories:
  - IT Articles
tags:
  - IT Stuff
  - linux
  - Ubuntu

---
If you have ever dreamed of having your own server, then I have good news. It has never been easier! In this tutorial I will discuss why you actually want to have your own server, how to setup your own Linux (Ubuntu) Server in less than 10 minutes and how to do this for free!

<!--more-->

## Why would you need your own server?

A dedicated server with root access opens a whole new world of applications, even if you are just browsing the internet. Here are some use cases:

**1. Webserver** -vIf you are hosting a website, it might be a good idea to move it to your own host, where you have full control.

**2. Code / file repository** - If you are going to collaborate with colleagues or friends on a project, it is crucial to have a common file repository. I've been using Subversion (SVN) for a long time, and it has proofed to be a viable partner.

**3. Save Internet browsing** - Is the local WiFi network at your favorite coffeehouse encrypted? If not, I recommend to route all your traffic through a Virtual Private Network (VPN). If you have your own server, it's quite easy to set up a VPN.

**4. Streaming Netflix** - Are you outside the United states? No problem, you can route the traffic from US based server through the VPN connection to your Computer, TV or iPhone, wherever you physically are.

**5. Experimentation** - instead of installing your stuff locally into Virtual Machines, try a server. With Amazon EC2 it's faster and more convenient.

These are just a few examples, to give you an idea about what you can do with your own server. Of course, the application of it is just limited to your imagination!

## Why Amazon EC2?

Amazon has not only emerged from a bookseller to a wholeseller,  it has also created one of the world's most powerful IT infrastructures in order to deliver it's own content in a fast & responsive way. Fortunately, Amazon has decided to sell these IT services to the public, as well. The are called [Amazon Web Services (AWS)][1] and consist by today of a wide variety of different services. For example, all the mp3 files of my podcast are stored and delivered through Amazon Simple Storage Service (S3). Another service is Amazon's Elastic Cloud Computer (EC2), which makes it really easy to create a virtual Server. Within a few mouse-clicks you can add almost infinite hard disk space or multiply the amount of CPUs, as you like (and as you can pay) 😉

**Best:** During the first year, a microinstance is with 10Gbyte of Harddisk is **completely free!**

All you have to do, is to [register your own Amazon AWS account][1].

## Let's get started

After creating your Amazon AWS Account, you need to register for EC2. The management console allows you to select predefined images (AMIs). There exists a wide range of predefined images. Feel free to select your favourite Linux distribution and follow the installation instructions. After less then 5 minutes, your Server instance is configured and ready to lauch:

{{< figure src="/img/2012/05/amazon_aws_instance_ready.jpg" link="/img/2012/05/amazon_aws_instance_ready.jpg" >}}

A minute later, your Server is up & running. Now you can connect yourself to the server and start configuring it.

## Make it even more convenient

A more convenient way however is to use an additional service called [Bitnami][2]. Bitnami allows you to preconfigure your server individually through a polished webinterface. Instead of installing the LAMP Stack (Linux, Apache, MySQL, PHP) by hand, Bitnami will do this for you. You just need to decide which kind of Linux Distribution you prefer and what you need on top (e.g. WordPress, Drupal, Joomla, etc). You just configure the server though Bitnami - it will be hosted directly on the AWS infrastructure, within your AWS Account. Here is a look the configuration looks like:

{{< figure src="/img/2012/05/bitnami_configuration_console.jpg" link="/img/2012/05/bitnami_configuration_console.jpg" >}}

Depending on the size of the instance and hard-disk, bitnami will show you automatically the estimated monthly cost. But again, if you are a new AWS client, a microinstance will be free for one year!

If you are setting up a remote server on Amazon AWS I suggest to use bitnami. The preconfigured images are very good and they provide a useful Wiki which guides you though the first steps. Bitnami will for example register a DNS record for you automatically so that you can access your server directly by SSH or through your webbrowser.

## Costs

Again, Amazon will give you a Micro Instance (2 cores & 613 MB Ram) one year for free. Uptime of your server is billed hourly. By today, an online hour for the instance costs 0,02 USD (free for the first year).  Incoming traffic is free, outgoing traffic costs a little bit (0,1USD / GByte).

I'm using the Iphone App called [Cloud Service Manager][3] to conveniently startup, shutdown or monitor my AWS instances.

## Final words

It has never been easier to set up your own server. All you need in an [Amazon AWS account][1] and your server will be up and running within a few minutes. There is plenty of good wikis and help available, however some basic Linux administration skills won't harm!

 [1]: http://aws.amazon.com
 [2]: http://bitnami.org
 [3]: http://itunes.apple.com/us/app/cloud-services-manager/id314316466?mt=8