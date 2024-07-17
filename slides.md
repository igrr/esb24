---
theme: seriph
highlighter: shiki
lineNumbers: false
transition: fade
title: Espressif Summit Brazil '24 — ESP-IDF and Tools Overview
layout: intro
addons:
  - "@katzumi/slidev-addon-qrcode"
  - slidev-addon-asciinema
canvasWidth: 800

---

# ESP-IDF and Tools Overview

## Ivan Grokhotkov<br>VP of Software Platforms @ Espressif

### 2024/07/17

---
layout: default
---

# Outline

<div class="grid grid-cols-2 gap-2">
<div>
<v-clicks>

- ESP-IDF overview
  - Philosophy behind IDF
  - What's inside
  - ESP Registry
- Overview of IDF subsystems
- Getting Started with development
- Tools

</v-clicks>
</div>

<div class="container mx-auto">
<img src="https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=https://igrr.github.io/esb24" class="object-center mx-auto py-10" width=180 height=180/>
<div class="text-center">

Slides: [https://igrr.github.io/esb24 <mdi-launch />](https://igrr.github.io/esb24)
</div>
</div>
</div>


---
layout: statement
---

# 🙋‍♂️ Have you developed using ESP-IDF?

---

# What is ESP-IDF

<v-clicks>

- Espressif IoT Development Framework
- An SDK for Espressif microcontrollers
- Developed since 2016, 84 releases made so far
- Is the first SDK to support new Espressif chips

</v-clicks>

---
layout: default
---

# ESP-IDF Philosophy

<v-clicks>

- **To provide good developer experience**
  - Sensible APIs, reasonable defaults
- **To be extensible**
  - Pluggable frameworks
- **To reduce development time**
  - Wide variety of ready-to-use features
- **To provide a path for production**
  - Manufacturing, provisioning, releases

</v-clicks>

---

# What's inside ESP-IDF

 <img src="/esp-idf-structure.png" class="w-150 rounded shadow" />

---
layout: iframe-right
url: https://components.espressif.com/components
class: text-left
---

# ESP Component Registry

<v-clicks>

- More than 400 public components
- Use components from Espressif and 3rd parties, or write your own
- Provides dependency and version management
- Ability to install private components from Git
- Lock file for reproducible builds

</v-clicks>


---

# Overview of ESP-IDF subsystems

- RTOS
- C library, POSIX
- Networking: LwIP, tcp_transport, esp_tls, MQTT, HTTP, esp-netif
- Connectivity: Bluetooth, Wi-Fi, 802.15.4, Ethernet
- Peripheral drivers
- Storage: partitions, filesystems, NVS
- OTA, Provisioning, Console
- Toolchain and Debugging


---

# FreeRTOS

<div class="grid grid-cols-2 gap-2">
<div>

- SMP support
- Integrated RISC-V and Xtensa ports
- Additional features (e.g. Ringbuffers)
- Optional pthread compatibility layer

</div>
<div>

![](/freertos.png)

</div>
</div>

---

# C library, POSIX

<div class="grid grid-cols-2 gap-2">
<div>

- Thread-safe newlib port
- Thread local storage
- C++23 with std::thread support
- Wide range of POSIX APIs provided
- Portability of software written for Linux

</div>
<div>

![](/newlib.png)

</div>
</div>


---

# Storage

<div class="grid grid-cols-2 gap-2">
<div>

- Partitions define Flash layout
- FAT, SPIFFS, LittleFS file systems integrated
- NVS — key-value storage for configuration and factory data
- File systems are mounted via VFS layer
- Flash Encryption can be used for data protection

</div>
<div>

![](/storage.png)

</div>
</div>


---

# Peripheral Drivers

<div class="grid grid-cols-2 gap-2">
<div>

- FreeRTOS-aware drivers
- Blocking and non-blocking modes of operation
- Flexible allocations of pins and channels

</div>
<div>

![](/peripherals.png)

</div>
</div>

---

# Connectivity

<div class="grid grid-cols-2 gap-2">
<div>

- Wi-Fi stack with Station and SoftAP modes
- ESP-NOW — connectionless protocol based on Wi-Fi
- Bluedroid (BT/BLE) and NimBLE (BLE only) stacks
- Standard-compliant BLE Mesh implementation
- 802.15.4 driver and OpenThread stack
- Extensible Ethernet MAC and PHY driver framework

</div>
<div>

![](/connectivity.png)

</div>
</div>

---


# Networking

<div class="grid grid-cols-2 gap-2">
<div>

- `esp-netif` network interface configuration layer
- LwIP TCP/IP stack
- `tcp_transport` and `esp_tls` abstraction layers
- MQTT client
- HTTP(S) client and server
- And more protocols available in [esp-protocols](https://github.com/espressif/esp-protocols) repository.

</div>
<div>

![](/networking.png)

</div>
</div>

---

# Application utilities

<v-clicks>
<div>

### OTA

- Can be used with any transport
- Image integrity and signature verification
- High-level functions for OTA from HTTPS

</div><div>

### Provisioning

- Wi-Fi network onboarding
- Supports BLE, Wi-Fi SoftAP, console transports
- Implements proof of possession and transport security

</div><div>

### Console

- Interactive console over UART, USB or network
- Custom commands registration, plus many commands provided

</div>
</v-clicks>

---

# Toolchain and Debugging


<div class="grid grid-cols-2 gap-2">
<div>

- Cross-compiler toolchains for GCC and RISC-V.
- JTAG debugging tools (OpenOCD, GDB).
- Run-time debugging features: panic handler, stack overflow guard, watchdogs.
- GDB Stub and Core Dump for postmortem debugging and remote diagnostics.
- SystemView and App Trace for application tracing.

</div>
<div>

![](/toolchain-debug.png)

</div>
</div>

---

# Getting Started with development

<v-clicks>

1. Prerequisites
1. Choosing the development environment
1. Installing
1. Exploring examples
1. Recommended reading
1. Combining features
1. Adding new components
1. Writing your own components

</v-clicks>

---

# Tools

<div class="grid grid-cols-2 gap-2">
<div>

- idf.py
- CMake build system
- monitor
- gdb, openocd
- qemu
- esptool, espefuse, parttool, otatool
- SPIFFS, FAT, LittleFS generators
- NVS generator and mfg-tool

</div><div>

- App trace
- Core dump
- GDB stub
- SystemView
- IDF Size
- Clang-tidy
- SBOM
- Docker image, CI integration
- Tools for testing (idf-build-apps, pytest-embedded)

</div></div>

---

| **Area** | **idf.py Commands** | 
| ---- | ---- |
| Configuration | `set-target`, `reconfigure`, `menuconfig` |
| Building | `build`, `app-build`, `bootloader-build` |
| Flashing | `flash`, `app-flash`, `bootloader-flash` |
| Monitor | `monitor` |
| Debugging | `openocd`, `gdb`, `coredump-info` |
| Size Analysis | `size`, `size-components`, `size-files` |
| Efuses | `efuse-summary`, `efuse-burn-efuse` |
| Emulation | `qemu` |
| Static Analysis | `clang-check` |

---

# `idf.py monitor` features

- Serial I/O
- Waiting for the device to reconnect
- Reset the board
- Re-build and re-flash without exiting the monitor
- Decode panic backtraces
- Decode core dump output
- Filter logging messages
- Save session log to file

---

# IDF Size

- Display application or component static Flash/RAM usage
- Compare Flash/RAM usage between versions of the app

```
    ┏━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
    ┃ Memory Type/Section   ┃ Used [bytes] ┃ Used [%] ┃ Remain [bytes] ┃ Total [bytes] ┃
    ┡━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
    │ Flash Code            │        80666 │     2.41 │        3261638 │       3342304 │
    │    .text              │        80666 │     2.41 │                │               │
    │ IRAM                  │        51835 │    39.55 │          79237 │        131072 │
    │    .text              │        50807 │    38.76 │                │               │
    │    .vectors           │         1027 │     0.78 │                │               │
    │ Flash Data            │        38224 │     0.91 │        4156048 │       4194272 │
    │    .rodata            │        37968 │     0.91 │                │               │
    │    .appdesc           │          256 │     0.01 │                │               │
    │ DRAM                  │        11236 │     6.22 │         169500 │        180736 │
    │    .data              │         8988 │     4.97 │                │               │
    │    .bss               │         2248 │     1.24 │                │               │
    └───────────────────────┴──────────────┴──────────┴────────────────┴───────────────┘

```

---

# IDF Clang-tidy

- Runs Clang-tidy static analysis tool on the project
- Integrates with idf.py (`idf.py clang-check`)
- Can be used in CI together with Github Code Scanning

![](/clang-tidy.png)

---

# Filesystem generators

<v-clicks>

- SPIFFS, FAT and LittleFS partitions can be generated during build process

  ```cmake
  fatfs_create_spiflash_image(storage-partition data-dir FLASH_IN_PROJECT)
  ```
  - `storage-partition` is defined in the partition table
  - `data-dir` subdirectory contains files to package
- `idf.py flash` will automatically flash the partition to the chip
- Can be used at production time for certificates, embedded websites, graphical assets

</v-clicks>

---

# NVS tools

- NVS generator: generate an NVS partition from CSV file of key-value pairs
- NVS parse: analyze the contents of an NVS partition
- Manufacturing tool: generate a set of NVS partitions based on CSV data file

<img src="/mfg-tool.png" class="w-150 rounded shadow" />

---

# Software Bills of Material (SBOM)

https://github.com/espressif/esp-idf-sbom

<v-clicks>

- Track software dependencies in a project
- Stay compliant with legal requirements (US EO14028, EU CRA)
- Create a list of open source licenses
- Look for known vulnerabilities in the dependencies
- Tool can be used with any ESP-IDF project

</v-clicks>

---

# Emulation

<v-clicks>
<div>

### QEMU

- Supports ESP32, ESP32-C3.
- `idf.py qemu monitor` — Launch and monitor the application inside QEMU emulator
- `idf.py qemu -g monitor` — Same, but with an emulated LCD framebuffer.
- `idf.py qemu gdb` — Debug the application inside QEMU using GDB

</div><div>

### Wokwi (https://wokwi.com/)

- Online simulator for all ESP chips
- Can be used in VS Code and in CI
- Can run any application for ESP — not only an ESP-IDF one

</div>
</v-clicks>

---

# CI and Testing

- [ESP-IDF Docker Image](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-docker-image.html) contains a complete environment to build IDF applications
- [esp-idf-ci-action](https://github.com/espressif/esp-idf-ci-action): can be used to easily build the project in Github CI
- [idf-build-apps](https://github.com/espressif/idf-build-apps) tool can be used to build multiple IDF applications in multiple configurations
- [pytest-embedded](https://github.com/espressif/pytest-embedded) is a Pytest plugin to simplify writing test harnesses
- [gh-esp-test-template](https://github.com/espressif/gh-esp-test-template): complete template of building and testing an application on Github
- [Wokwi](https://docs.wokwi.com/wokwi-ci/getting-started) can also be used in CI, also together with pytest-embedded

---
layout: intro
---

# Q&A

## Thank you for your attention!

---

# New in IDF and plans

- Driver-NG
- Clang compiler
- Network offloading
- Storage: NAND Flash, Journalling
- Hints
- TEE framework
- FreeRTOS upstream SMP
- ULP improvements
- Camera, graphics and LCD support
- QEMU

