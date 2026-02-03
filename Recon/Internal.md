# Internal Reconnaissance – Router Device

In this part i start working with router with less expected by producent way

## 1. UART

I first used a Comidox USB Logic Analyzer to observe the boot sequence. The only information I was able to extract at this stage was the Linux kernel version and the firmware version.

![IMG_20260119_132908](https://github.com/user-attachments/assets/036671b7-1fc4-45ad-bde8-644cc702cb43)

Later, I connected an IZOKEE CP2102 USB‑to‑UART adapter in an attempt to obtain a shell. However, in the newer firmware versions this access appears to be blocked.

<img width="4000" height="2252" alt="image" src="https://github.com/user-attachments/assets/9aa1999a-30a7-47f0-8829-87f2c3406b1e" />
