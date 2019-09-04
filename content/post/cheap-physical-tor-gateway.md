---
title: "Cheap Physical Tor Gateway"
date: 2018-05-04T21:22:25Z
draft: true
---
## Introduction

Recently I was browsing [Amazon](https://www.amazon.com) for a new home router that I could flash with [OpenWRT](https://openwrt.org/). Ideally I wanted a home router that I could easily flash with OpenWRT, had at least four ethernet ports, and had 802.11AC support (which is hard to find with OpenWRT). I did end up finding what I needed and it has been working great, but that's not the point of this post. While browsing Amazon I saw this funny looking, tiny, bright yellow "Mini Travel Router" from a company I had never heard of called [GL.iNet](https://store.gl-inet.com/). I had inadvertently found a router that supported another project I had in mind: Building a Tor/OpenVPN gateway device.

Let's begin by saying that when I say OpenWRT I could also mean [LEDE](https://lede-project.org/). It's a little confusing and not really something that anyone needs to worry about presently. LEDE is a fork of OpenWRT and it appears they got in some arguments but have now made up and have merged.

## The Hardware

The funny little yellow travel router is a GL.iNet [GL-MT300N-V2 Mini Smart Router](https://store.gl-inet.com/collections/travel-routers/products/gl-mt300n-v2-mini-smart-router).

The travel router has the following specifications:
* LEDE pre-installed
* 128MB RAM
* 16MB Flash Storage
* 2 Ethernet Ports
* 1 USB Port
* Programable Hardware Switch
* 5V/1A power not included by default - but any micro USB cable will probably work

Not too shabby for only $20.

## The Software

Plug it in and wait for it to fire up and you should see the Wifi network with the default key listed on the bottom on the device. Even easier is to plug in the WAN Ethernet port to your current network and your computer to the LAN Ethernet port. After your computer has an IP Address in the 192.168.8.0/24 range browse to 192.168.8.1 and you will be greeted with the default GL.iNet web interface. This looks fairly slick and has the most popular settings readily available, but we are just going to wipe this sucker out and flash it with OpenWRT.
