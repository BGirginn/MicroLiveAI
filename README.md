# MicroLiveAI • STM32F4-Discovery ─ AI-Assisted Live Optimisation  
*(LoRa node / Gateway reference design)*

![platform](https://img.shields.io/badge/MCU-STM32F407VG-168%20MHz-blue)
![license](https://img.shields.io/badge/license-MIT-green)
![tinyml](https://img.shields.io/badge/TinyML-TFLite--Micro-orange)

**MicroLiveAI** is a proof-of-concept project that shows how a  
*Cortex-M4*-based LoRa node can

* sample its own ISR and heap load every few milliseconds,  
* run a lightweight **TinyML** model on-chip (or on an optional ESP32-C3 co-processor), and  
* patch RAM or flash parameters **on-the-fly** — cutting airtime and CPU usage with **zero cloud dependency**.

---

## ✨ Key Features

| ✔ | Description |
|---|-------------|
| Real-time **cycle-accurate tracing** via DWT + SWO |
| 128 B **ring-buffer “stat block”** sampled at 1 – 5 kHz |
| **TFLite-Micro + CMSIS-NN** INT8 model (< 40 kB flash, < 16 kB RAM) |
| Action map: LoRa SF switch, heap-pool grow/shrink, ISR priority tweak |
| Atomic RAM patch **or** 128 kB **overlay flash sector** hot-swap |
| Roll-back & ECDSA-P256 signature check for safety |
| Optional **ESP32-C3 copro** for sub-ms inference |

---

## 🛠 Hardware

| Qty | Part | Notes |
|-----|------|-------|
| 1 | **STM32F4-Discovery** (STM32F407VG) | On-board ST-Link/V2-1 |
| 1 | **SX1276/78 LoRa module** | SPI + GPIO |
| 1 | Micro-USB cable | Power + SWD/SWO |
| – | *(Optional)* ESP32-C3 dev-kit | UART/SPI link as AI copro |
| – | Breadboard & jumper wires | Rapid prototyping |

---

## 💻 Software

* **STM32CubeIDE ≥ 1.15** (GNU Arm 12.3-rel1 toolchain embedded)  
* **Python 3.10** + `tensorflow==2.17.0` for model training  
* **OpenOCD** (bundled with CubeIDE) – SWO viewer / flash patcher  
* **CMSIS-NN 5.9.0** – automatically pulled by CubeIDE  
* **RadioLib** (or Semtech driver) – LoRa HAL layer

---

## ⚡ Quick Start

```bash
# 1. clone and open the project in CubeIDE
git clone https://github.com/BGirginn/MicroLiveAI.git
cd MicroLiveAI

# 2. build & flash
#    (CubeIDE → Project > Build, then Debug/Run)

# 3. open SWV ITM Console (168 MHz core, 2 MHz SWO)
#    observe ISR time and heap stats streaming every 1 ms
