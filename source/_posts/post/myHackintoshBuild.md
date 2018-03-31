---
title: With 1% effort to build 99% working Hackintosh
date: 2018-04-2 13:29:37
categories: mac
tags: [mac, hackintosh]
---

This is my 2017 Hackintosh build. I was using GTX 970 before but I just switch to Vega 64 recently. And it works out of box!!! That's the key to the whole build. With Vega GPU, you don't have to worry about tricky bugs any more. We just need to set up a clean build.

# Parts list

* Case: [Phanteks Eclipse Series P400 Stell ATX](https://www.amazon.com/gp/product/b01blhp5hs/ref=oh_aui_detailpage_o00_s00?ie=utf8&psc=1)
* Mobo: [Gigabyte GA-Z270X-UD5](https://www.amazon.com/gp/product/b01mryhw6b/ref=oh_aui_detailpage_o01_s00?ie=utf8&psc=1)
* CPU: [i7 7700K](https://www.amazon.com/gp/product/b01mxsi216/ref=oh_aui_detailpage_o01_s02?ie=utf8&psc=1)
* Cooler: [Corsair Hydro Series H100i v2](https://www.amazon.com/gp/product/b019exssbg/ref=oh_aui_detailpage_o01_s01?ie=utf8&psc=1)
* GPU: [Sapphire Nitro+ Radeon RX Vega 64](https://www.newegg.com/Product/Product.aspx?Item=N82E16814202321&cm_re=vega_64-_-14-202-321-_-Product)
* SSD: [Samsung 960 EVO](https://www.amazon.com/gp/product/b01lyfkjr7/ref=oh_aui_detailpage_o01_s00?ie=utf8&psc=1)
* RAM: [Ballistix Sport LT](https://www.amazon.com/gp/product/b01b4f3ijy/ref=oh_aui_detailpage_o01_s00?ie=utf8&psc=1)
* HDD: [WD Black 1TB](https://www.amazon.com/gp/product/b00fjrs6fu/ref=oh_aui_detailpage_o01_s01?ie=utf8&psc=1)
* WIFI&BT: [fenvi FV-T919(802.11AC Desktop Wifi Card)](https://www.amazon.com/gp/product/b01mdlg51u/ref=oh_aui_detailpage_o01_s01?ie=utf8&psc=1)
* PW: [Corsair CX750M](https://www.amazon.com/corsair-cx750m-bronze-haswell-modular/dp/b00alk3kem/ref=sr_1_1?s=electronics&ie=utf8&qid=1497980491&sr=1-1&keywords=corsair+cx+750m)

<!--more-->

![](https://ws2.sinaimg.cn/large/006tNbRwgy1fpzd05a4bvj30wk0jo0ui.jpg)

# Building

For the build, the liquid cooler cannot fit in the top of the case with this special motherboard. I remove the front fan and put it at the top of the case. Then I install the liquid cooler up front the case.

# Installation

I just follow the installation from [Tonymacx86 High Sierra Installation](https://www.tonymacx86.com/threads/unibeast-install-macos-high-sierra-on-any-supported-intel-based-pc.235474/) and that's works for me.

The SMBIOS setting I'm using is iMac 14,2. I was using iMac 18,3 before but once I switch to Vega graphics card, it will cause black screen. So I suggest to stick with 14,2.

The only issue I have is the audio. I am not sure it's the macOS version 10.13.4's problem or Vega graphics card's. A quick fix is using USB to headphone jack converter. You can buy anyone from [Amazon](https://www.amazon.com/s/ref=nb_sb_noss_1?url=search-alias%3Daps&field-keywords=usb+to+audio).

In 90% cases, you can go ahead update your system without any problem. But be careful, and check out [Tonymacx86's update posts](https://www.tonymacx86.com/forums/os-x-updates.32/). For example, you might have to update your clover bootloader or replace your old apfs.efi to the new one.
