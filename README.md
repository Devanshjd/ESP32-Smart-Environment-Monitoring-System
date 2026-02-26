# ESP32-Smart-Environment-Monitoring-System
ESP32 IoT environment monitor using DHT22 with RGB humidity status, buzzer alerts, and interrupt-driven manual override via slide switch.
ESP32 Smart Environment Monitoring System is an embedded IoT project that continuously monitors temperature and humidity using a DHT22 sensor and provides real-time user feedback via an RGB LED and a buzzer. The system is designed using non-blocking timing (millis) for responsive behaviour. It includes an interrupt-driven slide switch that toggles manual override mode for user control of the RGB LED.

This project demonstrates practical embedded engineering skills: sensor integration, PWM control via ESP32 LEDC channels, interrupt handling with debouncing, state management, and reliable real-time behaviour.

What the system does (clear functional requirements)
Inputs

DHT22 sensor reads:

Humidity (%)

Temperature (°C)

Slide switch (interrupt) toggles manual mode ON/OFF

Outputs

RGB LED indicates humidity range

Buzzer alerts when humidity is high

Serial Monitor prints readings for debugging/logging

Status logic (rules)
Automatic mode (default)

RGB colour shows humidity state:

Green: humidity ≤ 60%

Yellow: 60% < humidity ≤ 75%

Red: humidity > 75%

Buzzer behaviour:

If humidity > 75%, buzzer toggles ON/OFF at a fixed interval (alert cadence)

If humidity drops back, buzzer turns OFF automatically

Manual Override mode (triggered by switch interrupt)

Automatic RGB indicator pauses

RGB cycles colours every 1 second (visual confirmation)

Sensor still reads and logs to Serial

Buzzer stays OFF (no alerts in manual mode)


Engineering decisions (why it’s good)

Non-blocking design: Uses millis() timers instead of delay() so the system stays responsive.

PWM brightness control: Uses ESP32 LEDC PWM channels for smooth RGB LED control.

Interrupt-driven input: Switch uses hardware interrupt so manual mode responds instantly.

Debouncing: ISR includes debounce window to prevent false toggles.

Fail-safe sensor handling: If DHT returns NaN, LED shows a distinct “error” colour.


ESP32 Smart Environment Monitoring System (IoT / Embedded)

Built an ESP32-based temperature and humidity monitoring system using a DHT22 sensor with real-time serial logging.

Implemented RGB LED humidity indicators using PWM (LEDC) with defined thresholds and error handling for sensor failures.

Developed buzzer alert logic for high-humidity conditions using non-blocking timers to maintain responsiveness.

Added interrupt-driven manual override via slide switch with debouncing and a colour-cycling user mode.

Validated and tested behaviour in Wokwi prior to deployment and refined for low-latency response.
