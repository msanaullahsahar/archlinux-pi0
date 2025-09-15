# Arch Linux Installation Guide for Raspberry Pi Zero W

This guide will help you install **Arch Linux armv6h** on your Raspberry Pi Zero W, both with a monitor/keyboard (direct setup) and headlessly (via Wi-Fi and SSH).

## 1. Preparation

1. **Download the image**  
   Download the `arch_linux_pi_zero.img` file.

2. **Burn the image to SD card**  
   Use [Balena Etcher](https://www.balena.io/etcher/) (or a similar tool) to burn the image onto your SD card.

## 2. Direct Setup (with Monitor & Keyboard)
1. Insert the SD card into your Raspberry Pi Zero W.
2. Connect the Pi to an HDMI screen and a USB keyboard/mouse.
3. Power on the Pi.
4. Login credentials:
   ```
   Username: root
   Password: 249840
   ```
5. Use `wifi-menu` in terminal to setup your wifi connection.

## 3. Headless Setup (Wi-Fi & SSH)

**To run your Pi Zero W without a monitor or keyboard:**

1. After burning the image, open the SD card's boot partition on your computer.
2. Create a plain text file named `wifi.txt` in the boot partition.
3. Add your Wi-Fi credentials in the following format (replace with your network info):
   ```
   SSID:PASSWORD
   ```
   Example:
   ```
   SaharWiFi:MySecretPass123
   ```
   **Notes:**
   - Only the first line of `wifi.txt` is used.
   - SSID and PASSWORD can include spaces and special characters.
   - No quotes are needed.
   - Use a colon `:` to separate SSID and PASSWORD.
   - The file will be automatically deleted after the Pi connects to Wi-Fi.

4. SSH is enabled by default.
5. Insert the SD card into your Pi Zero W and power it on.
6. Connect via SSH:
   ```bash
   ssh root@<Pi_IP_address>
   Password: 249840
   ```
   
## 4. Expanding the Root Filesystem
After logging in, expand the root partition to use the full SD card:
1. Open a terminal and run:
   ```bash
   fdisk /dev/mmcblk0
   ```
2. Inside fdisk, use the following commands:
   ```
   p   → print partition table
   note start sector of partition 2 (p2)
   d   → delete partition 2
   n   → create new partition 2, use the same start sector, default end (max)
   w   → write changes
   ```
3. Resize the filesystem:
   ```
   resize2fs /dev/mmcblk0p2
   ```
Your root partition now uses the full SD card capacity.

### 5. Open an issue if you need help. (This guide is upto date as of September 15, 2025)

## ✅ Done! Your Raspberry Pi Zero W is now running Arch Linux ARM and ready for use.
