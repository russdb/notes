### 1. Form Factors

|**Form Factor**|**Description**|**Included Components**|**Primary Use Case**|
|---|---|---|---|
|**SoC (The Chip)**|The raw silicon integrated circuit (IC) (e.g., ESP32-D0WD).|Bare chip.|Requires complex soldering, external circuits, and an antenna to function.|
|**Module**|Ready-to-integrate module (e.g., ESP32-WROOM-32).|Adds Flash memory, a crystal oscillator, an antenna, and shielding.|Designed to be integrated directly into custom printed circuit boards (PCBs).|
|**Development Board**|A complete prototyping board (e.g., ESP32-DevKitC).|Adds a USB-to-UART bridge, voltage regulators, Boot/EN buttons, and pin headers.|Ready for immediate prototyping, testing, and breadboard use.|

### 2. ESP32 Chip Families & Capabilities

| **Chip Family / Series**          | **Core Architecture & Speed**      | **Wireless Connectivity**                                                  | **Key Features & Ideal Use Cases**                                                                           |
| --------------------------------- | ---------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Original ESP32**                | Dual-Core Xtensa @ 240 MHz         | Wi-Fi 4 + BT Classic/BLE                                                   | Mature, cheap, and has the highest GPIO count. Good for general-purpose IoT.                                 |
| **ESP32-S3** _(Performance & AI)_ | Dual-Core Xtensa @ 240 MHz         | Wi-Fi 4 + BLE 5                                                            | AI acceleration (SIMD), Native USB, camera & display support. Best for edge AI, cameras, and screens.        |
| **ESP32-C3** _(Low-Cost RISC-V)_  | Single-Core RISC-V @ 160 MHz       | Wi-Fi 4 + BLE 5                                                            | Cost-effective and secure. A modern, low-power upgrade to the original ESP32.                                |
| **ESP32-C5** _(High-Efficiency)_  | Single-Core RISC-V @ up to 240 MHz | **Dual-Band Wi-Fi 6 (2.4 GHz & 5 GHz)** + BLE 5 + Zigbee/Thread (802.15.4) | Designed for congested networks requiring 5 GHz Wi-Fi capabilities alongside modern smart home mesh support. |
| **ESP32-C6** _(Smart Home)_       | Single-Core RISC-V @ 160 MHz       | **Wi-Fi 6 (2.4 GHz only)** + BLE 5 + Zigbee/Thread                         | Smart home mesh (Matter over Thread/Wi-Fi). Great for IoT networks.                                          |
| **ESP32-H2** _(Battery & Mesh)_   | Single-Core RISC-V @ 96 MHz        | Zigbee + Thread + BLE **(NO WI-FI)**                                       | Ultra-low power, mesh-only. Ideal for battery-powered smart sensors & Zigbee/Matter nodes.                   |

### Key Differences: ESP32-C5 vs. ESP32-C6

While both the C5 and C6 are modern, single-core RISC-V chips built for smart home and IoT mesh applications (both supporting Zigbee, Thread, and Matter), they have two major hardware distinctions:

- **Wi-Fi Frequency Bands:** The **ESP32-C6** only operates on the crowded **2.4 GHz** Wi-Fi band. The **ESP32-C5** introduces **Dual-Band Wi-Fi 6**, allowing the device to connect to either **2.4 GHz or 5 GHz** networks. This makes the C5 ideal for environments with heavy 2.4 GHz interference.
        
- **Processing Power:** The **ESP32-C6** is clocked at **160 MHz**, which is sufficient for typical sensors and relays. The **ESP32-C5** features a faster processor clocked up to **240 MHz**, giving it a performance edge for more demanding tasks.