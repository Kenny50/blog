+++
title = 'Debugging Android, how to connect to local server'
author = '張永翰'
description = 'connection between android device with local server'
date = 2024-03-26T14:01:55+08:00
tags = ['Android', 'Emulator']
+++

TL;DR port is same as server defined, the key is change to ip address

1. emulator — 10.0.2.2
2. Using ip — (required same network environment) type ifconfig | grep "inet "| grep -v 127.0.0.1 in terminal, copy something like 192.168.0.7
3. Port forwarding — (require usb connection) open `chrome://inspect/#devices` in chrome, check remote target detected your device, setup port forwarding like port: 9999 ipaddress and port : 127.0.0.1:9999

---

## Emulator — special alias

We have to connect to different ip while we tested our android in a different environment with a local server. Before we dive into this article, a quick discussion will be helpful. While we type localhost in chrome, we can access the network interface via loopback on the host, and the localhost is actually the name of ip 127.0.0.1 .

Now we start from a simple one, an emulator, while we start an emulator, we actually create an android OS in our computer, if we use localhost or 127.0.0.1 inside the emulator, it will loopback to android itself, and find nothing. The 10.0.2.2 is a preserved ip special alias to your host loopback interface(127.0.0.1 on your development machine) .

---

## Using ip — required same network environment

The wireless debug is more tricky, the connection between android phone and computer is not related to wireless debug, is related to the same internet environment, when a device connects to a Wi-Fi network, it is assigned an IP address by the router. This IP address is unique to that device on the network and can be used to communicate with other devices on the same network.

---

## Port forwarding — require usb connection

The last one is Usb debug mode, in the page “chrome://inspect/#devices” , port forwarding is used to route traffic from a website or web application running on a connected device to the development machine running Google Chrome.

However, even though I wrote port forwarding in USB mode, but using usb doesn’t impact ip solution, I prefer using ip more than using port forwarding.

[Android doc](https://developer.android.com/studio/run/emulator-networking)