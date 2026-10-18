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


## ⚠️ Known Hardware Quirks & Bench Workarounds

### 1. USB-C Power Delivery (PD) Negotiation Failure (0V Rail Output)
* **Observed Quirk:** Connecting the board directly to modern USB-C Power Delivery (PD) chargers (e.g., Anker Nano 30W GaN) or laptop USB-C ports via a **USB-C to USB-C cable** results in no power delivery (board remains completely unpowered).
* **Root Cause:** PCB layout omits the standard dual $5.1\text{k}\Omega$ pull-down resistors on the `CC1` and `CC2` pins. Modern smart PD controllers detect floating CC pins and refuse to initialize the 5V power rail.
* **Lab Workaround:** 
  - Power the board using a **USB-A to USB-C cable** connected to a standard 5V USB 2.0/3.0 port or standard 5V wall adapter.
  - Alternatively, use a USB-C to USB-A adapter inline to force the 5V bus high.

---

### 2. Automated Serial Bootloader Handshake Failure (`esptool` Hang)
* **Observed Quirk:** Executing terminal flashing commands via `esptool.py` results in infinite connection retries (`Connecting...____....____`), failing to automatically enter ROM bootloader mode.
* **Root Cause:** Insufficient RC timing capacitance ($0.1\mu\text{F}$ instead of $1\mu\text{F}$–$10\mu\text{F}$) or transistor logic failure on the DTR/RTS auto-reset circuit between `EN` (RST) and `GPIO0` (BOOT).
* **Lab Workaround (Manual Boot Timing Method):**
  1. Plug the board into your Linux host via USB.
  2. Initiate your `esptool.py` flash command in the terminal.
  3. Immediately press and hold the physical **`BOOT`** button on the back of the board.
  4. Tap the **`RST`** (Reset) button once while continuing to hold **`BOOT`**.
  5. Release **`BOOT`** as soon as `esptool.py` displays `Connecting...` and begins writing flash chunks.

---

### 📺 Display Driver Identification
* **Aliens / Generic Budget Units:** Boards with the `TPM408-2 8` display glass marking typically use the **ILI9341** display driver.
* **Branded / Specialty Units (e.g., NerdMiner):** Units with the `H685` marking are known to use alternative drivers like **ST7789**. 
* **Lab Warning:** Flashing firmware configured for the wrong display driver results in a blank or solid white screen. Always verify your hardware's display panel marking before compiling or flashing custom binaries.
