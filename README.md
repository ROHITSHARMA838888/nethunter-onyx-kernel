# 🐉 Kali NetHunter GKI Kernel for POCO F7 ("onyx")

![Android](https://img.shields.io/badge/Android-17%20%7C%2015-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Kernel](https://img.shields.io/badge/Kernel-6.6%20GKI-blue?style=for-the-badge&logo=linux&logoColor=white)
![Page Size](https://img.shields.io/badge/Page%20Size-4KB-orange?style=for-the-badge)
![Root](https://img.shields.io/badge/Root-KernelSU--Next-red?style=for-the-badge)
![License](https://img.shields.io/badge/License-GPL--2.0-yellow?style=for-the-badge)

A high-performance, security-focused **Kali NetHunter GKI (Generic Kernel Image)** custom kernel built specifically for the **POCO F7 (`onyx`)** running **Infinity OS (Android 17)**, AOSP, and HyperOS with **Linux Kernel 6.6**.

Engineered with complete support for modern Wi-Fi penetration testing dongles, packet injection, and USB HID attack emulation.

---

## 🌟 Key Features

* **GKI 2.0 Architecture**: Retains 100% vendor hardware compatibility (Touch, Camera, Fingerprint, Audio, and Display will not break).
* **4KB Page Size (`CONFIG_ARM64_4K_PAGES=y`)**: Custom-tailored for 4K ROMs like **Infinity OS** to guarantee zero bootloops.
* **Full Wireless Injection**: `mac80211` packet injection patch applied for seamless monitor mode.
* **BadUSB / DuckHunter**: `CONFIG_USB_CONFIGFS_F_HID=y` enabled for USB Keyboard and Mouse attack emulation.
* **KernelSU-Next / APatch Ready**: Native kernel-level root support without tripping Android 17 SELinux security rules.

---

## 📡 Supported External Wi-Fi Adapters & Chipsets

Out-of-the-box drivers and firmware modules included:

| Hardware Dongle | Chipset | Driver Module | Features |
| :--- | :--- | :--- | :--- |
| **TP-Link Archer T2U Plus (AC600)** | Realtek RTL8821AU / 8811AU | `8821au.ko` | 2.4GHz + 5GHz Dual-Band, High Gain, Monitor Mode |
| **Alfa Network AWUS036ACH** | Realtek RTL8812AU | `8812au.ko` | AC1200 High Power Dual-Band, Packet Injection |
| **TP-Link TL-WN722N (v1)** | Atheros AR9271 | `ath9k_htc.ko` + FW | Native Monitor Mode & Frame Injection |
| **Alfa Network AWUS036NHA** | Atheros AR9271 | `ath9k_htc.ko` + FW | Legendary Penetration Testing Adapter |
| **TP-Link TL-WN722N (v2 / v3)** | Realtek RTL8188EUS | `8188eu.ko` | Aircrack-ng patched monitor mode driver |
| **Alfa Network AWUS036NEH** | Ralink RT3070 | `rt2800usb.ko` + FW | Long Range 2.4GHz Wi-Fi Injection |
| **Mini Wi-Fi Dongles** | Ralink RT5370 / MT7601U | `rt2800usb.ko` / `mt7601u.ko` | Ultra-compact Wi-Fi monitoring |

---

## 🚀 How to Build on GitHub Actions (1-Click Cloud Build)

You do **NOT** need a high-end Linux PC or 30GB of disk space. This repository compiles directly using GitHub's free Cloud Runners.

1. **Fork** or **Clone** this repository to your GitHub account.
2. Ensure the workflow file is present at:
   ```
   .github/workflows/build-nethunter-onyx.yml
   ```
3. Navigate to the **Actions** tab on your GitHub repository.
4. Select **"Build POCO F7 Onyx NetHunter GKI 6.6 Kernel"** on the left menu.
5. Click **"Run workflow"** -> Select `main` branch -> Click green button.
6. In **12–15 minutes**, the compilation completes.
7. Scroll down to the **Artifacts** section at the bottom of the completed action and download:
   ```
   NetHunter-Kernel-POCO-F7-Onyx-AllWifi.zip
   ```

---

## 📲 Installation / Flashing Guide

### Prerequisites:
* Unlocked Bootloader on your POCO F7 (`onyx`).
* Installed Custom Recovery (**OrangeFox** or **TWRP**).
* Active Infinity OS (Android 17) or compatible AOSP ROM.

### Flashing Steps:
1. Transfer `NetHunter-Kernel-POCO-F7-Onyx-AllWifi.zip` to your phone's internal storage or OTG drive.
2. Reboot into **OrangeFox / TWRP Recovery**.
3. *(Highly Recommended)* Go to **Backup** -> Select **Boot** -> Swipe to Backup your current stock kernel.
4. Go to **Install** -> Select `NetHunter-Kernel-POCO-F7-Onyx-AllWifi.zip`.
5. **Swipe to Flash**.
6. **Reboot System**.

---

## 🧪 Post-Install Verification

Connect your external Wi-Fi dongle (e.g. TP-Link Archer T2U Plus or Alfa) using an OTG adapter and verify in terminal:

```bash
# 1. Verify Kernel Version
uname -r
# Output should indicate GKI 6.6 with NetHunter patches

# 2. Check if USB Dongle is detected
lsusb

# 3. Check Wireless Interface
ip link show

# 4. Enable Monitor Mode on external adapter
sudo airmon-ng start wlan1

# 5. Start packet sniffing
sudo airodump-ng wlan1
```

---

## ⚠️ Disclaimer

* This kernel is designed for security research, authorized penetration testing, and educational purposes only.
* Always obtain written authorization before testing networks you do not own.
* The maintainers are not responsible for any misuse or bricked devices. Flashing custom software always carries inherent risks.

---

## 🤝 Credits & Acknowledgements

* **Google AOSP**: Android Common Kernel (ACK) GKI 6.6
* **Kali NetHunter Team**: NetHunter wireless stack & HID patches
* **osm0sis**: AnyKernel3 universal flasher
* **aircrack-ng & morrownr**: RTL8812AU and RTL8821AU modern Linux drivers
* **KernelSU Team**: Kernel-based root solution for Android GKI
