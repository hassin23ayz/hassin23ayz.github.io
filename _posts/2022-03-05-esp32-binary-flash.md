---
layout: post
title: esp32 flash
published: true
date: 2022-03-05
categories: [firmware]
tags: [esp32]
---

1. Download**Flash Download Tools**

**![](https://lh4.googleusercontent.com/Xtrk7B_fZylOeGXYQESR3MPchflKJVBiX3pIjBFqWaMbpRr9IHH5ctVOvQSa1wvaBjpVNNBomJGtMGC-N2BaO4R6WKHicQ0VKc8glDVnCDQtj2DaPz9go6hM_JGHnd66qAaU01Ex)**

from<https://www.espressif.com/en/support/download/other-tools>

  


2. The upload the 4 bin files to gDrive or copy them from ubuntu machine to this windows machine ( all these files are in build folder )

Todo : attach image from git repo

The files are

  


![](https://lh5.googleusercontent.com/othQzvogpbrthSH5RybDz1bTQ_1Z7njFtRIp-UscdZcVw3ztnflkUQCY4nkhNNULk6ld-TPDb_gv3EdqMpeYWt0dqlObInjl8njb2IDNSZ7kUAU8ExITNZhkzQzUpip6KBiqyzE9)

3. Run the installer

![](https://lh5.googleusercontent.com/-k4Kl6c9vtk2o0gSYeGAN8zCBPUHCzwwuzYFd46ue_wdy879qqhUpLFN-yajURdlD46KAC_0fBFHWKZHZgRaYWaaoPP_KuDrBKfiPoeBZRouawBbSrq6IWb1-Xi03t_EqznHlO6X)

![](https://lh6.googleusercontent.com/YC1y4J4UauTP8Gb4jRZkW67-DOy6IdcFmOW8ZmqvDL4dLhJYhWNudOgwMT8jm4co9ujAcw7GARmHp89Ma00B5Ggt4EaMto5srf9byrEAdxtbRHzN_GIPgxXo4KOLVgydXveoD9Hb)

Then open the bin files and put the following address

Check all the checked marks

  
  


![](https://lh4.googleusercontent.com/W_Kc8cel34tk8q9pVBrJ-Yuv0ZGKPiyuGSF_2PwNrGrZGbyJVbIn2RxWACC6NDI4Jc_Do_77BE1fDSFt1Jg_Mt6E7Y1HsRsV6bXBhGiq5VQhL8pyOsI1rzpIkJmrzZ_9ppai7ls9)

The Addresses are

| bootloader.bin       | 0x1000  |
| -------------------- | ------- |
| esp32_mesh.bin       | 0x10000 |
| ota_data_initial.bin | 0xD000  |
| partitions.bin       | 0x8000  |

  
  
  
  
  
  
  
  
  
  
  


Hold down the**boot**button and then press Start

After Flashing gets completed the Finish state will be shown as below

![](https://lh3.googleusercontent.com/PeBM0BNJj5ExQCTTZmioqz9-un2vj-t8WcQQlM4dJdC1kxd26SQfIcv6ouwFYWO5CisTHQoVC3xLuyzYTyEmc1BAsSZzGOelQMXpBXXy6tbJZ5Ee9tNOK6-Yz3iurf5Ugl5kLkA3)

Click Stop button and close the application

Then open putty

![](https://lh6.googleusercontent.com/a488bL-tL_nlXHkh-D2evahr5EQgjxxxGXSFW72JPgaNWl1ixHj6neFugBa4kUpxzppZKAl4mv2pN3AX-j6Ey8Naic2dBq9pnsu6t72PsqarJM_27vnlW8PImvpHzXfZnZBREAvC)

  
  
  
  
  


And check the debug output

![](https://lh6.googleusercontent.com/YcSZsSSb9Nuiozhkce7htr9PPkWFXHEC52K2XIuiPfAwNxQ34yzM1i1vXsBzbFjl-FJrp20XBtdTly9HMy-_RzwvGQP7WM_7_21JjbOgkTcd3fIhyJOv2Dmfckw4ChkBtwcOgKVF)

  
  
  
  
  
