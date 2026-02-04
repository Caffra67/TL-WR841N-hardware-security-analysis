# Firmware

The firmware was obtained via OSINT after an unsuccessful attempt to extract it using SPI.
Initial analysis shows that the beginning of the .bin file contains the same information as observed during the UART boot sequence.

The remaining part of the file appears as unreadable data, which suggests that it is either encrypted or compressed.
```
$ strings -n 10 TL-WR841Nv14_PL_0.9.1_4.19_up_boot\[241230-rel52464\].bin 
#$#& ##& $#* ##* $#. ##. $#2 ##2 4#6 3#6 3
$##.""#."##2""#2"##6""#6"##:""#:"C
(pE`{pC`$j
bootcmd=tftp
bootdelay=1
baudrate=115200
ethaddr="00:0A:EB:13:09:69"
ipaddr=192.168.0.2
serverip=192.168.0.225
U-Boot 1.1.3 (Dec 30 2024 - 14:30:00)
raspi_read_devid
bbu_spic_trans
bbu_spic_busy_wait
raspi_unprotect
raspi_wait_ready
raspi_4byte_mode
raspi_read
bbu_mb_spic_trans
diff_dly=%d
overwrite %x
[%02X%02X%02X%02X]
[%04X%02X%02X][%08X][00%04X%02X]
DU Setting Cal Done
*** failed ***
relocate_code Pointer at: %08lx
Please choose the operation: 
   %d: Load system code to SDRAM via TFTP. 
   %d: Load system code then write to Flash via TFTP. 
   %d: Boot system code via Flash (default).
   %d: Load Boot Loader code then write to Flash via TFTP. 
0x80200000
0x80100000
 Please Input new ones /or Ctrl-C to discard
        Input device IP 
        Input server IP 
        Input Uboot filename 
        Input Linux Kernel filename 
0x80A00000
### ERROR ### Please RESET the board ###
[...]
L27Yqi\ IHNRY$
u#op^|@>UJ
gfpXO           uD]
*       j"dckrQ7.f
8}Os!<(lf_
4m6GBN 4P2
S/ZcGvh#<g
BB/Y\1Z;+z
 V''RhHq?g]
GpncYl=TC?
*w$CSMc [
```
We can see that the firmware image contains three main parts of interest.
The first part is U-Boot, which acts as the bootloader.
The second part is the Linux kernel, stored as LZMA-compressed data.
The third part is the root filesystem, stored as a SquashFS image, which contains the operating system files.

```
└─$ binwalk TL-WR841Nv14_PL_0.9.1_4.19_up_boot\[241230-rel52464\].bin 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
54544         0xD510          U-Boot version string, "U-Boot 1.1.3 (Dec 30 2024 - 14:30:00)"
66560         0x10400         LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 2986732 bytes
1049088       0x100200        Squashfs filesystem, little endian, version 4.0, compression:xz, size: 2989940 bytes, 551 inodes, blocksize: 262144 bytes, created: 2024-12-30 06:34:44
```

After that, I checked the entropy of the file and identified three areas of interest.
For clarification, an entropy value close to 1.0 indicates that the data is likely compressed or encrypted, which makes extraction and further analysis more difficult.

<img width="636" height="475" alt="image" src="https://github.com/user-attachments/assets/17d3c35e-8f50-4c23-8455-cf55afc79c07" />

 
