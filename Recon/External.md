# External Reconnaissance – Router Device

This phase focuses on identifying the target device and collecting all available information prior to any active interaction or exploitation.
The router is treated as a disposable test device and will not be exposed to production or external environments.

## 1. Device Identification

![IMG_20260119_003254](https://github.com/user-attachments/assets/276ebea9-3cb7-470e-9334-f3879cce5797)

Based on the physical inspection of the device, the following components were identified:

**1 Ground (GND)** reference point

**2 ESMT M13S2561616A-AST1P5FK** – DDR SDRAM

**3 MediaTek MT7628NN** – System on a Chip (SoC)

**4 cFeon QH328-104HIP** – SPI NOR Flash memory

**5 UART interface** – exposed for serial communication

The device operates on a 9V power supply.

## 2. Router info

<img width="4000" height="2252" alt="IMG_20260119_002404" src="https://github.com/user-attachments/assets/82270ec3-eddb-40b8-8034-6a9148dce07e" />

The following information was obtained from labels and physical markings on the router:

**Model:** TP-LINK TL-WR841N (PL)

**LAN MAC Address:** 98:03:8E:F1:CF:A6

**WAN MAC Address:** 98:03:8E:F1:CF:A7

**Default Wi-Fi Password:** 34618769

**SSID:** TP-Link_CFA7

## 3. Nmap

After connecting the router to the internet, I scanned it with nmap to identify exposed services.

```
[ Oguri ~ ]$ nmap -T4 -p- -A 192.168.0.1
Starting Nmap 7.98 ( https://nmap.org ) at 2026-01-27 18:12 +0000
Nmap scan report for 192.168.0.1
Host is up (0.042s latency).
Not shown: 65531 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     Dropbear sshd 2012.55 (protocol 2.0)
| ssh-hostkey: 
|   1024 01:fb:49:6a:85:68:c1:28:97:d7:08:35:c6:b8:bf:8d (DSA)
|_  1039 2e:ca:fa:73:40:5f:3d:d7:ac:d5:01:88:e7:0e:40:dd (RSA)
53/tcp   open  domain?
80/tcp   open  http    TP-LINK WAP http config
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
1900/tcp open  upnp    Portable SDK for UPnP devices 1.6.19 (Linux 2.6.36; UPnP 1.0)
Service Info: OS: Linux; Device: WAP; CPE: cpe:/o:linux:linux_kernel, cpe:/o:linux:linux_kernel:2.6.36
```
**Port 22/tcp** 
The device uses Dropbear SSH version 2012.55, which is outdated.
While researching this version, I found multiple known vulnerabilities (CVE), for example:
https://www.tenable.com/plugins/nnm/6338

**Port 53/tcp** 
At this stage it is difficult to determine the exact implementation, but this port is most likely used as a DNS resolver or DNS forwarder for the local network.

**Port 80/tcp**
This port exposes the TP-LINK administrative web interface, which is accessible over HTTP.

**Port 1900/tcp**
UPnP is enabled on the device, allowing automatic port forwarding without authentication.
Due to the age of the UPnP implementation and the underlying Linux kernel, this service may introduce additional attack surface.
