---
title: Projects
permalink: /projects/
layout: page
sitemap: false
---

## _Android based wireless Oscilloscope_
A low cost portable Pen shaped handheld oscilloscope converts analog signal into digital signal and communicates with an Android Application over bluetooth channel written in java. The Android Application works as the GUI/Front end of an actual oscilloscope. 

<https://www.youtube.com/watch?v=zUco-ubSN4c&t=2s>

<br>
## _Zero-Conf LED Controller_
Bonjour/Zero-conf network protocol is a self discovery protocol within an intra network. Multiple RGB LED controllers are connected in a local network over wifi or ethernet medium. A central PC software was developed in QT5 to control the LED controllers

<br>
## _OBD2 Vehicle Reader_
Wrote a firmware in C to sniff CAN bus of the vehicle using MCP2501 CAN ic
Interfaced with elm327 OBD2 ic via AT commands and logged vehicle Data
[toyota-axio and Mitsubishi car model tested]

<br>
## _BLE Weight Scale_
NRF51822 BLE mcu interfaced with a small load cell measures applied load and in turn calculates the mass. Android App communicates via BLE GATT profile
Battery Powered device with low power consumption 

<br>
## _Magnetic Levitation_
Implemented PD algorithm to control the current passing through an electromagnet in order to
magnetically levitate a metal plate. 
<https://youtu.be/PNfhhsShYOA>

<br>
## _Pile Load Capacity Testing Logger_
Interfaced [Matest] Pressure transducer and a Linear actuator with calibration option
KS108 graphic LCD was interfaced to show real time data. The collected data was encoded as json packet and sent over REST Interface
<https://youtu.be/PNfhhsShYOA>

<br>
## _Network Booting of Android x86_
Custom Android Linux Kernel Build modifying network level device drivers 
Coreboot-iPXE & NFS (Network File System) integration
Uniform Android OS porting to HP-probook & Nexus-7 Tablet
<https://whileinthisloop.blogspot.com/2019/08/network-booting-ubuntu-using-ipxe-and.html>

<br>
## _GPS Tracking Device_
Interfaced SIM908 GSM-GPS module with AVR microcontroller. The Device sends message to user's mobile phone number if geo-location gets changed by a certain limit

<br>
## _Wireless Sensor Network_
Multiple NRF24L01 2.4GHz module enabled Nodes measures water flow detection inside drainage system using flow meter sensor and pushes data to a master node in a star topology. Master Node had a SIM800 GSM/GPRS module and acted as the gateway. The Project was part of a Smart City Bootcamp Program 

<br>
## _Fire Detection And Alarm System_
Industrial fire Alarm monitoring sensor nodes using MQ-2 sensor
Nodes were Connected to a central controller over long distance RS485 cable [ multi drop ]. To ensure data integrity HDLC framing, FCS were added. The master controller has DOT Matrix Display to show Unit Names in rotation. 
This industrial device is now in operation at <https://www.nestle.com.bd/> factory. 

<br>
## _Smart Pump controller_
Performs On-Off controlling of Motor sensing water level via high power float switch. Measures the Energy used by the motor and calculates Bill upon it. 
Shows Parameters, values and water level with animation on graphical LCD

<br>
## _Frequency Counter & RPM meter_
Calculates a waveform’s period
Counts the number of rotations of motor by reflective sensor

<br>
## _Humidity and Temperature sensor based Control Device_
Interfaced HSM-20G sensor and LM-35.
Device turns on/off pump based on humidity and moisture.
Quadratic equation was implemented in the firmware . [equation at MATLAB]

<br>
## _Remote controlled DOT matrix Display_
IR remote and dot matrix display was interfaced for a Restaurant food order process. RF433 RF modules were interfaced to transmit container IDs to a central unit.  

<br>
## _Timer Based Controller_
Custom Controller made for a Candy factory
Low Cost Alternative of previous PLC based system
User could set time & order of operations 
8 output Relay channel

<br>
## _Lift controller_
Implemented the general purpose Lift logics in a low cost controller
7 segment display was interfaced
4 Cargo Lift controllers are running across 2 industries in Bangladesh 

<br>
## _OTA Bootloader upgrade stack_
A Bootloader stack was written in C/assembly as a modular firmware component (OTA) for one of the products of <https://www.codegate.co.uk/> .The Boot-loader code can read pre-saved binary from the external flash/sd-card & perform firmware upgrade [offline]

[Matest]: <https://www.matest.com/en/>






