---
layout: post
title: Building an AOSP image
published: true
date: 2019-09-10
categories: [android]
tags: [software]
---

Here In this Post I will be sharing how I downloaded Android AOSP sources and built AOSP image for Nexus 7 [2012] device. You can follow this approach to build AOSP images for your devices for example Nexus 5 . So Let’s Start

# Device Information

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSn6q33QaKzbik3Y3ySfOiPvRysxOU5wffs0A&usqp=CAU" >


* The Tablet device used here is the Nexus 7 (2012)
* OS : Android-Lollipop
* Product Name : grouper
* Variant : grouper
* HW version : ER3
* Bootloader Version : 4.23

# Environment Setup

* install some required packages

```bash
ayx@ayx-HP:~$ sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip
```

```bash
ayx@ayx-HP:~/$ sudo apt-get install ncurses-dev
```

* install adb tool

```bash
ayx@ayx-HP:~/$ sudo apt-get install android-tools-adb
```

* Fix Udev permission error

```bash
ayx@ayx-HP:~$ lsusb
```

* check the vendor id left of the colon , e.g nexus 5 & Open this file

```bash
ayx@ayx-HP:~$ sudo gedit /etc/udev/rules.d/51-android.rules
```

* Put the following at the bottom of the file and save

```bash
# Nexus 5 Google Inc
SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", MODE="0666", GROUP="plugdev"`
```

```bash
ayx@ayx-HP:~$ sudo chmod a+r /etc/udev/rules.d/51-android.rules
ayx@ayx-HP:~$ sudo service udev restart
ayx@ayx-HP:~$ fastboot -l devices
ayx@ayx-HP:~$ sudo service udev restart
ayx@ayx-HP:~$ sudo udevadm control --reload-rules
ayx@ayx-HP:~$ sudo udevadm trigger
ayx@ayx-HP:~$ fastboot -l devices`
```

* install Java 7

```bash
ayx@ayx-HP:~$sudo apt-get install -f
ayx@ayx-HP:~$sudo add-apt-repository ppa:openjdk-r/ppa
ayx@ayx-HP:~$sudo apt-get update
ayx@ayx-HP:~$sudo apt-get install openjdk-7-jre
```

* select java 7 for the followings

```bash
ayx@ayx-HP:~$ sudo update-alternatives --config javac
ayx@ayx-HP:~/$ sudo update-alternatives --config java
ayx@ayx-HP:~/$ sudo update-alternatives --config javap`
```

* check versions of following & In my cases these were the versions