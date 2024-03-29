---
layout: post
title: Bufferbloat In Router
published: true
date: 2022-04-06
categories: [web]
tags: [networking]
featured_img: "https://upload.wikimedia.org/wikipedia/commons/thumb/e/e3/ResidentialGatewayCloseup.jpg/320px-ResidentialGatewayCloseup.jpg"
sitemap:
  lastmod: 2022-04-18
  priority: 0.5
  changefreq: 'monthly'
---

### _Better Speed makes better user engagement_

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e3/ResidentialGatewayCloseup.jpg/320px-ResidentialGatewayCloseup.jpg" width="480" height="420" style="display: block; margin: 0 auto">

### Background 
Routers are everywhere & today I want to share some background on an interesting problem named **Bufferbloat** which plays a crucial role in router's performance. This is a concept that was first coined by Jim Gettys in 2010. Before discussing About it let us first dive into some basics 

<br>
When a packet is transmitted from an end user device it first reaches to the Home Router. There, the packet gets decoded and next desitination IP:Port gets set . Afterwards the packet travels to Routers external to the home network for example the ISP router . With similar decoding the subsequent Routers gets the packet and finally the packet reaches the destination IP. Each Router has to decode the packet and before the decoding process the packet gets queued in Router's memory . There are numerous intermediate Routers that a packet needs to encounter while travelling from source to destination and this is how Each Router plays a significant role to the overall latency.

<br>
- _what is Latency ?_
> The time for a packet to travel from source to destination 

There are 4 kinds of delay affecting the latency, these are

| **Delay Types** | **Depends On** |
| ------ | ------ |
| Propagation delay | The medium through which the signal travels & the distance between source and destination|
| Transmission Delay | Packet lengh & Available Data Rate of the transmitting Link |
| Processing Delay | Time required by the Router for Processing packet header & determining  packet's destination  |
| Queuing Delay  | If packets are arriving at a faster rate than the router is capable of then they are queued inside the buffer resulting in a delay |

<br>

- _so what is BufferBloat ?_

As each Router has to process a lot of incoming packets so it keeps a large amount buffer memory to keep all the packets in queue. **Bufferbloat** actually refers to the Queuing delay. When a large amount of packets are queued in router's memory then at a point the memory gets full and remain full at congested links. 

- _so How should we solve BufferBloat ?_

One may think that increasing the buffer memory would solve the problem but the actual irony is that, this phenonmenon does not get solved by increasing Router's memory but rather it gets worsened. To better understand this interesting fact you can read more here  [Bufferbloat](https://www.bufferbloat.net/projects/bloat/wiki/Introduction/). As a developer you should apply Proper Queuing Algorithm. For example In order to tackle this problem CoDel Active Queue Managment Algorithm has been implemented in Linux 3.5+ kernels thus As an Ideal Router Manufacturer one needs to spot it and take necessary steps in the Router Firmware / OS kernel. 

This is an active problem and many routers have this problem affecting the overall latency. The Network Operators should also audit network operated under them from time to time and keep proper maintenance . [Required Steps](https://www.bufferbloat.net/projects/bloat/wiki/What_can_I_do_about_Bufferbloat/) . 

<br>