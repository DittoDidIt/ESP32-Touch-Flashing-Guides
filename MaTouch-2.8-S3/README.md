# 📡 Makerfabs MaTouch 2.8" (ESP32-S3) Evaluation & Documentation

> **Maintained by:** Ditto Did It Labs (D.I.T.T.O.)  
> **Status:** Hardware Evaluation In Progress (Sample Arriving)  
> **Partner:** Makerfabs  

---

## 📋 Overview
This section serves as the central documentation hub for the **Makerfabs MaTouch 2.8" Display (ESP32-S3 series)**. It provides detailed hardware specs, serial flashing protocols, USB interface behaviors, and open-source firmware compatibility benchmarks.

---

## 🛠️ Key Evaluation Objectives
- [ ] **Power Rail Inspection:** Validate USB-C CC resistor ($5.1\text{k}\Omega$) compliance for USB-C to USB-C (PD) powering.
- [ ] **USB Interface Verification:** Test Native USB (CDC/JTAG) vs. Hardware UART serial behavior on Linux systems.
- [ ] **Boot & Flashing Logic:** Document auto-reset mode behavior and stable `esptool` baud rate thresholds.
- [ ] **Display & Touch Performance:** Benchmark SPI/Parallel display bus performance and capacitive/resistive touch responsiveness under custom GUI firmwares.
- [ ] **Peripheral Testing:** Map pinout interfaces (I2C, SD card bus, Grove/HY2.0 expansion headers).

---

## 📁 Section Contents
- [`specs-and-pinout.md`](./specs-and-pinout.md) – Chipset specs, pin mapping, and power requirements.
- [`flashing-guide.md`](./flashing-guide.md) – Step-by-step flashing guide for `esptool.py` and web flashers.
