# External Recon Router Devices

This phase answers one question:

*What can we learn about the device before touching it?*

## 1. Device Identification

![IMG_20260119_003254](https://github.com/user-attachments/assets/276ebea9-3cb7-470e-9334-f3879cce5797)

- **1** Ground 
- **2** ESMT M13S2561616A-AST1P5FK **DDR SDRAM**
- **3** MEDIATEK MT7628NN 2502-AFSL BCMS73JR **SoC (System on a Chip)**
- **4** cFeon QH328-104HIP **FLASH (SPI NOR)**
- **5** UART connection

- Divace operate at 9V

## 2. Router info

<img width="4000" height="2252" alt="IMG_20260119_002404" src="https://github.com/user-attachments/assets/82270ec3-eddb-40b8-8034-6a9148dce07e" />

- Model:TL-WR841N(PL)
- LAN MAC: 98-03-8E-F1-CF-A6
- WAN MAC: 98-03-8E-F1-CF-A7
- Basic Password: 34618769
- SSID: TP-Link_CFA7
## 3. Nmap

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
