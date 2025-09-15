Arch Linux ARM Setup Guide for Raspberry Pi Zero W

This guide will help you set up Arch Linux ARM on your Raspberry Pi Zero W, both with a monitor/keyboard (direct setup) and headlessly (via Wi-Fi and SSH).

1. Preparation

Download the image
Download the arch_linux_pi_zero.img file.

Burn the image to SD card
Use Balena Etcher
 (or a similar tool) to burn the image onto your SD card.

2. Direct Setup (with monitor & keyboard)

Insert the SD card into your Raspberry Pi Zero W.

Connect the Pi to an HDMI screen and a USB keyboard/mouse.

Power on the Pi.

Login credentials:

Username: root
Password: 249840

3. Headless Setup (Wi-Fi & SSH)

If you want to run your Pi Zero W without a monitor or keyboard:

After burning the image, open the SD card's boot partition on your computer.

Create a plain text file called wifi.txt in the boot partition.

Add your Wi-Fi details in the following format (replace with your credentials):

SSID:PASSWORD


Example:

SaharWiFi:MySecretPass123


Important Notes:

Only the first line of wifi.txt is used.

SSID and PASSWORD can include spaces and special characters.

No quotes are needed. Use a colon (:) to separate SSID and PASSWORD.

The file will be automatically deleted after the Pi connects to Wi-Fi.

SSH is enabled by default.

Insert the SD card into your Pi Zero W and power it on.

Connect via SSH:

ssh root@<Pi_IP_address>
Password: 249840

4. Expanding Root Filesystem

After logging in, expand the root partition to use the full SD card:

Open a terminal and run:

fdisk /dev/mmcblk0


Commands inside fdisk:

p   → print partition table
note start sector of partition 2 (p2)
d   → delete partition 2
n   → create new partition 2, use the same start sector, default end (max)
w   → write changes


Resize the filesystem:

resize2fs /dev/mmcblk0p2
