# STM32F407-Discovery LCD Firmware

This is a firmware project for the STM32F407-Discovery board driving a 16x2 character LCD based on the HD44780U controller with an external extension chip.

The project was developed using STM32CubeIDE and is intended to be a clean and reusable starting point for HD44780-compatible LCDs on STM32 platforms (see the Notes section below).

## 📦 Hardware

- **Board:** STM32F407-Discovery
- **MCU:** STM32F407VG
- **LCD:** 16x2 character LCD
- **LCD Controller:** HD44780U + extension chip

## 🔌 Pin Configuration

| LCD Pin   |     STM32 Pin     |              Notes                |
|-----------|-------------------|-----------------------------------|
| VSS       | GND               | Circuit GND                       |
| VDD       | 5V                | Circuit Positive                  |
| V0        | GND               | Connected through a potentiometer |
| RS        | GPIOA_1           | Register Select                   |
| E         | GPIOA_2           | Enable                            |
| RW        | GPIOA_3           | Read/Write                        |
| D0-D7     | GPIOE_7-GPIOE_14  | 8-bit mode                        |
| A         | 5V                | Anode                             |
| K         | GND               | Cathode                           |

## 🧠 Features

- HD44780-compatible LCD driver
- 8-bit mode support (4-bit mode is not supported)
- Clear, modular LCD driver code
- Easily portable to other STM32 MCUs
- CubeMX / `.ioc` driven configuration

## 🛠️ Software Environment

- **IDE:** STM32CubeIDE
- **HAL Library:** STM32 HAL
- **Language:** C
- **RTOS:** None

## 🚀 Getting Started

1. Clone the repository:
   ```
    git clone https://github.com/UtkuGokalp/stm32-lcd-firmware.git
   ```
2. Open STM32CubeIDE and import the project:
   ```
    File -> Import -> Import STM32 Project -> STM32CubeIDE Project -> Select your local project folder
   ```
3. Build and flash the project to the board

## 📌 Notes

### 🔧 Debug Features Left Enabled
During development, **USB CDC** and the **onboard LEDs** were used for debugging purposes. To make future development and debugging easier, they are left enabled by default.

If you do not need these features, they can be safely disabled as described below.

### 💡 Disabling Onboard LEDs

1. Open `LCD_Driver.ioc`
2. Locate pins **PD12–PD15**:
   - `LED_GREEN`
   - `LED_ORANGE`
   - `LED_RED`
   - `LED_BLUE`
3. Left-click each pin and set it to **`Reset_State`**

✅ Onboard LEDs are now disabled.

### 🔌 Disabling USB CDC

1. Open `LCD_Driver.ioc`
2. Navigate to:
   - `System Core → RCC → High Speed Clock (HSE)`  
     → Set to **Disabled**
3. Navigate to:
   - `Connectivity → USB_OTG_FS → Mode`  
     → Set to **Disabled**
4. Navigate to:
   - `Middleware and Software Packs → USB_DEVICE → Class For FS IP`  
     → Set to **Disabled**
5. Open `main.c` and remove both the declaration and the definition of the following function:
   
   ```c
   void USBD_CDC_Receive(uint8_t* buf, uint32_t* len);
   ```
✅ USB CDC is now fully disabled.

### 🐧 Platform Notes

This project was developed and tested on Linux. While it should work on Windows and macOS, these platforms have not been tested and issues may occur.

## 📄 License
This project is released under the MIT License.

## 🤝 Contributions
Contributions, bug reports, and suggestions are welcome. Feel free to fork the project and submit a pull request.
