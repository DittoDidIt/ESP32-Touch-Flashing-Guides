# ⚡ MaTouch 2.8" (ESP32-S3) Flashing & Recovery Guide

> **Lab:** Ditto Did It Labs  

---

## 🐧 Linux Command-Line Flashing (`esptool.py`)

### 1. Identify System Port
Connect the device to your Linux host and check port enumeration:
```bash
ls -l /dev/ttyACM* /dev/ttyUSB*
