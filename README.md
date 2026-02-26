# ESP32 Smart Environment Monitoring System (DHT22 + RGB + Buzzer + Interrupt Switch)

A practical ESP32 IoT project that monitors **temperature & humidity** using a **DHT22** sensor and provides instant feedback using:
- **RGB LED** status (humidity levels)
- **Buzzer** alerts (high humidity)
- **Slide switch interrupt** for **manual override** of the RGB LED

This repo is designed to be **GitHub + CV ready** and works in **Arduino IDE**, **PlatformIO**, and can be adapted to **Wokwi**.

---

## Features

- Reads DHT22 every ~2 seconds (recommended interval)
- Humidity status via RGB LED:
  - **Green**: humidity ≤ 60%
  - **Yellow**: 60% < humidity ≤ 75%
  - **Red**: humidity > 75% (also triggers buzzer)
- Buzzer alert toggles on/off at a fixed cadence when humidity is high
- Slide switch uses an **interrupt** to toggle **Manual Override** mode:
  - Manual mode cycles colours every 1 second
  - Automatic humidity indication pauses (sensor still logs to Serial)

---

## Wiring (Typical)

| Component | ESP32 Pin |
|---|---|
| DHT22 DATA | GPIO 15 |
| RGB Red | GPIO 25 |
| RGB Green | GPIO 26 |
| RGB Blue | GPIO 27 |
| Buzzer | GPIO 14 |
| Slide Switch | GPIO 33 |
| 3V3 | DHT22 VCC, RGB Anode (if common anode adjust logic), switch side |
| GND | DHT22 GND, buzzer GND, RGB cathode (if common cathode) |

**Important:** If your RGB LED is **common anode**, invert the PWM values (255 -> OFF).  
Current code assumes **common cathode** RGB (most common in basic kits).

---

## How To Run (Arduino IDE)

1. Install **ESP32 board package** in Arduino IDE.
2. Install library: **DHT sensor library** (Adafruit) + Adafruit Unified Sensor (if requested).
3. Open:
   - `src/esp32_environment_monitor.ino`
4. Select Board: **ESP32 Dev Module**
5. Upload and open Serial Monitor at **115200**.

---

## How To Run (PlatformIO)

1. Install PlatformIO extension (VS Code)
2. Open this folder in VS Code
3. Build/Upload using PlatformIO tasks.

---

## Files

- `src/esp32_environment_monitor.ino` — main firmware
- `diagram.json` — optional Wokwi diagram template (edit pins if needed)
- `libraries.txt` — Arduino library list
- `platformio.ini` — PlatformIO build config
- `requirements.txt` — kept for repo completeness (notes only)

---

## Customisation

Edit thresholds in code:

```cpp
static const float HUMIDITY_OK_MAX   = 60.0;
static const float HUMIDITY_WARN_MAX = 75.0;
```

Change pins as required at the top of the `.ino`.

---

## Tips 

- Show humidity changing triggers LED transitions
- Flip the switch to demonstrate interrupt/manual override
- Mention debounce + non-blocking `millis()` design

---

## Author

Devansh Jamdar  
LinkedIn: https://linkedin.com/in/devansh-jamdar-34b6b620b
