# ESP32 Touch Display Master Flashing & Troubleshooting Guide

> **Maintained by:** Ditto Did It Labs (D.I.T.T.O.)  
> **Contact:** dittodidit.labs@gmail.com  
> **Hardware Target:** ESP32 / ESP32-S3 Touch Displays (CYD & Makerfabs MaTouch Series)

---

## 1. Overview & Drivers Setup

Before flashing custom firmware (such as ESP32 Marauder, SquatchWatch, HaleHound, or Bruce), ensure the correct USB-to-UART bridge drivers are installed for your board's serial chip:

* **CH340 / CH341 Drivers:** Common on standard Cheap Yellow Displays (CYD).
* **CP210x Drivers:** Common on ESP32-S3 boards, including Makerfabs MaTouch series.

> ⚠️ **Troubleshooting Serial Ports:** If your terminal or flasher reports `Failed to connect to ESP32: Timed out waiting for packet header`, verify that your USB cable supports **data transfer** and is not power-only.

---

## 2. Boot Mode Execution Sequences

Different ESP32 hardware revisions require specific physical button combinations to enter the onboard bootloader:

### Method A: Standard Auto-Reset Trigger
1. Connect the board via USB.
2. Hold down the **`BOOT`** button (IO0).
3. Press and release the **`RESET`** (EN) button once.
4. Release the **`BOOT`** button.
5. Initiate flashing in Web Flasher or Esptool.

### Method B: Cold Boot / Pre-Power Trigger
1. Disconnect the USB cable.
2. Press and hold the physical **`BOOT`** button.
3. Plug in the USB cable while continuing to hold **`BOOT`**.
4. Release the **`BOOT`** button after 2 seconds.

### Method C: Sustained Hold Trigger (Stubborn Drivers)
1. Hold **`BOOT`** continuously throughout the entire writing phase until the terminal output reaches 100% verification.

---

## 3. Partition Schemes & Flash Settings

When flashing compiled binaries (`.bin` files) using Esptool or Web Flashers:

* **Flash Frequency:** `80MHz`
* **Flash Mode:** `DIO` (or `QIO` for high-performance S3 parallel displays)
* **Erase Flash:** Recommended `Erase All Flash Before Sketch Upload` on initial setup to clear corrupted NVS partitions.

---

## 4. Hardware Reference & Support

For questions, firmware porting assistance, or documentation feedback, reach out to **Ditto Did It Labs** at `dittodidit.labs@gmail.com`.
