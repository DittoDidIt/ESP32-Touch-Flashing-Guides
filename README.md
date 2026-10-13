# ESP32 & MaTouch Display Flashing & Troubleshooting Hub

> **Maintained by:** Ditto Did It Labs (D.I.T.T.O.)  
> **Contact:** dittodidit.labs@gmail.com  
> **Purpose:** Comprehensive hardware quick-start guides, driver setup workflows, and custom open-source firmware documentation for ESP32 touch display hardware (including standard CYD and Makerfabs MaTouch ESP32-S3 series).

---

## 📌 Featured Guides & Documentation

- [x] **[Master Flashing & Troubleshooting Guide](./ESP32_Master_Flashing_Guide.md)** – Universal guide covering CP210x/CH340 drivers, manual `BOOT` sequences, and partition schemes.
- [ ] **Makerfabs MaTouch ESP32-S3 Guide** – *(In Progress)* Setup and pinout mapping for parallel/RGB display buses.
- [ ] **Firmware Porting Guides** – Notes on running ESP32 Marauder, SquatchWatch, HaleHound, and Bruce.

---

## 🛠️ Boot Mode & Hardware Sequence Reference

Different ESP32 touch display boards require specific physical boot button sequences depending on their USB-to-UART auto-reset circuitry:

1. **Standard Sequence:** Hold `BOOT` → Press & release `RESET` → Release `BOOT`.
2. **Pre-Power Sequence:** Hold `BOOT` before inserting USB cable → Insert cable → Release `BOOT`.
3. **Sustained Hold Sequence:** Hold `BOOT` continuously throughout the entire firmware write cycle until verification hits 100%.

---

## 📷 Hardware Builds & Test Benches

*Active setups running custom firmware builds:*

| Board Revision | Display Controller | Active Firmware |
| :--- | :--- | :--- |
| **Standard CYD (2.8")** | ST7789 / SPI | ESP32 Marauder |
| **Standard CYD (2.8")** | ST7789 / SPI | SquatchWatch (LVGL) |
| **MaTouch ESP32-S3** | Parallel / RGB | *(Upcoming Evaluation & Guide)* |

---

## 🤝 Open Source & Hardware Vendor Collaboration
This repository provides free, accessible documentation to lower setup barriers and reduce product return rates for open-source hardware makers and distributors.
