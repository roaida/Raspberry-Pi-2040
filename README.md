# 🔌Raspberry Pi RP2040 Minimal Board (Sponsoredby PCBWay)

A compact, minimal circuit design for the Raspberry Pi RP2040 microcontroller. This board includes essential components for booting, programming via USB, and running custom embedded applications.
---

## 📦 Features
- ✅ RP2040 Dual-core ARM Cortex-M0+ MCU (QFN-56)
- 💾 16MB QSPI Flash (W25Q128JVSIQ)
- 🔋 3.3V LDO Regulator (NCP1117)
- 🔌 USB interface for power and programming
- ⏱️ 12 MHz Crystal Oscillator
- 🎚️ Exposed GPIO headers for external interfacing
- 🧰 BOOTSEL and RESET jumper logic
- 🧪 SWD interface for debugging (optional)
---

## 🧠 Working Mechanism

### 1. **Power Supply**
- USB 5V (VBUS) enters via micro USB (J1).
- The **NCP1117** regulator converts 5V → 3.3V.
- 3.3V powers the **RP2040**, **flash**, and **I/O**.

### 2. **Clock Generation**
- A 12 MHz crystal oscillator (U1) provides the reference clock.
- RP2040 uses this to generate internal system clocks via PLL.

### 3. **Boot Process**
- RP2040 checks `QSPI_SS` (Pin 56) during reset:
  - **HIGH** → Boot from QSPI Flash (U4)
  - **LOW** → Enter BOOTSEL (USB Mass Storage Mode)
- Code is read directly from flash using **QSPI** interface.

### 4. **Firmware Upload**
- Short the **USB_BOOT jumper (P3)** and toggle the **RUN pin** to enter BOOTSEL mode.
- Upload `.UF2` firmware file directly via USB.

### 5. **Program Execution**
- Once booted, the MCU runs user code:
  - Controls GPIO
  - Reads ADC (GPIO26–29)
  - Communicates via USB, UART, I2C, SPI, etc.

### 6. **Debugging (Optional)**
- **SWD/SWCLK** pins exposed for JTAG/SWD debugging tools.
---

## 🧩 Key Components

| Ref | Component | Description |
|-----|-----------|-------------|
| U3  | RP2040    | Main microcontroller |
| U4  | W25Q128JV | 16MB QSPI Flash |
| U2  | NCP1117   | 3.3V LDO Regulator |
| U1  | ABM8-272-T3 | 12 MHz Crystal Oscillator |
| J1  | USB       | Power & USB communication |
| R2, R3 | 27Ω     | USB D+ / D− termination |
| Cx  | Capacitors | Power filtering & stability |
| P1, P2 | Headers | GPIO & ADC access |
| P3  | Jumper    | USB_BOOT selector |

---

## 🗺️ Schematic & PCB
- ✅ Included in `/hardware/PI.SchDoc` and `/hardware/PI.PcbDoc`
- Designed using **Altium Designer**
- Compact layout optimized for signal integrity and EMI performance

---

## 🔧 How to Use
1. Connect via USB.
2. Short `USB_BOOT` jumper and toggle `RUN` to enter BOOTSEL mode.
3. Drag and drop your `.UF2` firmware file.
4. Board reboots and runs your program.
---

