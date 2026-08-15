# STM32 Environmental Monitoring System

An embedded environmental monitoring system built using an **STM32F303K8 microcontroller** and **BME280 environmental sensor**. The system measures temperature, humidity, and atmospheric pressure and displays the readings on a multiplexed 4-digit 7-segment display.

A push button allows the user to cycle between measurements, while a **UART serial interface** provides live sensor readings and system-state information for monitoring and debugging.

---

## Demo

<img width="800" height="450" alt="STM32_BME280_Monitor_Gif" src="https://github.com/user-attachments/assets/cceb2637-765e-4611-ac23-82b07597f6f7" />

The demonstration shows the system cycling between temperature, pressure, and humidity readings while simultaneously outputting sensor data and the current system state over UART.

▶️ **[Watch the full project demonstration on LinkedIn](https://www.linkedin.com/posts/angelozyh_stm32-embeddedsystems-embeddedc-ugcPost-7493907560077451264-7WY-)**

---

## Features

* BME280 temperature, humidity, and atmospheric pressure measurement
* I2C communication between the STM32 and BME280
* Multiplexed 4-digit 7-segment display
* Dual 74HC595 shift-register display control
* Push-button interface for cycling between measurements
* Software button debouncing
* Timer-based display multiplexing
* UART serial monitoring and debugging
* Interrupt-driven button input and timing
* BME280 calibration and compensation calculations

---

## Hardware

| Component                     | Purpose                                     |
| ----------------------------- | ------------------------------------------- |
| **STM32 NUCLEO-F303K8**       | Main microcontroller                        |
| **BME280**                    | Temperature, humidity, and pressure sensor  |
| **4-digit 7-segment display** | Displays sensor measurements                |
| **2× 74HC595**                | Shift registers for controlling the display |
| **Push button**               | Cycles between measurement modes            |
| **Breadboard**                | Circuit prototyping                         |
| **Resistors / capacitors**    | Display and supporting circuitry            |

---

## Software & Tools

* **C**
* **STM32 HAL**
* **STM32CubeIDE**
* **STM32CubeMX**
* **Git / GitHub**
* **UART serial terminal**

---

## System Overview

The STM32 communicates with the **BME280 over I2C** to retrieve raw temperature, pressure, and humidity measurements.

The raw sensor values are converted into usable measurements using the BME280's factory calibration parameters and compensation formulas.

The resulting measurement is formatted and displayed on a **4-digit 7-segment display**. Two **74HC595 shift registers** reduce the number of GPIO pins required to control the display.

A push button cycles the system between three display states:

**Temperature → Pressure → Humidity → Temperature**

Sensor readings and the current system state are also transmitted over **UART**, providing a serial interface for monitoring and debugging.

---

## Peripheral Usage

| STM32 Peripheral | Function                           |
| ---------------- | ---------------------------------- |
| **I2C**          | BME280 sensor communication        |
| **UART**         | Serial monitoring and debugging    |
| **GPIO**         | Shift-register and display control |
| **Timer**        | 7-segment display multiplexing     |
| **EXTI**         | Push-button interrupt handling     |

---

## Display Control

The 4-digit 7-segment display is controlled using **two 74HC595 shift registers**.

The STM32 shifts serial data into the registers to control the display segments and digit selection while requiring fewer GPIO pins than direct parallel control.

A hardware timer drives the multiplexing process, rapidly switching between digits to create the appearance that all four digits are illuminated simultaneously.

---

## Button Control

The push button cycles through the available measurement states:

```text
Temperature → Pressure → Humidity → Temperature
```

Button input is handled using an **external interrupt (EXTI)** with software debouncing to prevent a single physical press from registering multiple state changes.

---

## UART Monitoring

UART provides a secondary interface for viewing sensor measurements and the current system state.

Example output:

```text
Temperature: 22.45 °C
Pressure: 995.24 hPa
Humidity: 41.25 %RH
State: humidity
```

The UART interface was also used throughout development to verify sensor communication and debug system behavior.

---

## What I Learned

This project gave me hands-on experience with:

* Configuring STM32 peripherals using STM32CubeMX
* Communicating with a digital sensor over I2C
* Reading and interpreting hardware datasheets
* Working with sensor registers and calibration data
* Implementing timer-driven display multiplexing
* Using shift registers to reduce GPIO requirements
* Handling external interrupts and button debouncing
* Using UART for embedded debugging
* Integrating multiple hardware and software components into a complete system
* Debugging interactions between firmware and physical hardware

---

## Repository Structure

```text
STM32-Based-Environmental-Monitoring-System/
├── Core/          # Application source code and headers
├── Drivers/       # STM32 HAL and CMSIS drivers
├── Debug/         # Build/debug output
├── .settings/     # STM32CubeIDE project settings
└── README.md
```

---

## Future Improvements

* Design a custom PCB to replace the breadboard prototype
* Add long-term sensor data logging
* Add configurable warning thresholds
* Create an enclosure for the system
