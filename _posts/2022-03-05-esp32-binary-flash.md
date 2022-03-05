---
layout: post
title: esp32 flash
published: true
date: 2022-03-05
categories: [firmware]
tags: [esp32]
---

1.  Download Flash Download Tools

![](images/image2.png)

from [https://www.espressif.com/en/support/download/other-tools](https://www.google.com/url?q=https://www.espressif.com/en/support/download/other-tools&sa=D&source=editors&ust=1646495739193929&usg=AOvVaw1BCpfiItGFs8YKDexdvChw) 

2.  The upload the 4 bin files to gDrive or copy them from ubuntu machine to this windows machine ( all these files are in build folder )

Todo : attach image from git repo

The files are

![](images/image4.png)

3.  Run the installer

![](images/image8.png)

![](images/image3.png)

Then open the bin files and put the following address

Check all the checked marks

![](images/image1.png)

The Addresses are

bootloader.bin

0x1000

esp32\_mesh.bin

0x10000

ota\_data\_initial.bin

0xD000

partitions.bin

0x8000

Hold down the boot button and then press Start

After Flashing gets completed the Finish state will be shown as below

![](images/image6.png)

Click Stop button and close the application

Then open putty

![](images/image7.png)

And check the debug output

![](images/image5.png)