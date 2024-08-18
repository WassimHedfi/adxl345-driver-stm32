# ADXL345 Driver for STM32 Nucleo-F446RE

This repository contains a custom driver for the ADXL345 accelerometer, interfaced via I2C with an STM32 Nucleo-F446RE board. The driver is implemented in a separate source and header file, making it easy to deploy on other STM32 boards or microcontrollers with minimal modification.

## Features

- **ADXL345 Driver**: A lightweight, efficient driver for the ADXL345 accelerometer, allowing easy communication over I2C.
- **I2C Interface**: The driver handles the setup and communication with the ADXL345 using the I2C protocol.
- **UART Transmission**: Acceleration data (`x_acc`, `y_acc`, `z_acc`) is read from the ADXL345 and sent over UART, enabling real-time data monitoring or further processing on other devices.
- **Modular Design**: The driver is structured in a modular way, with separate source and header files, enabling easy integration into different projects or with other STM32 microcontrollers.

## Getting Started

### Prerequisites

- **STM32 Nucleo-F446RE**: The target microcontroller board for this project.
- **ADXL345 Accelerometer**: A 3-axis accelerometer with I2C communication.
- **STM32CubeIDE**: Recommended IDE for development and compilation.
- **UART Interface**: For monitoring or processing the accelerometer data on a connected device.

### Hardware Setup

1. **Connect the ADXL345 to the STM32 Nucleo-F446RE**:
   - **VCC** to **3.3V**
   - **GND** to **GND**
   - **SCL** to **I2C1_SCL** (Pin PB8)
   - **SDA** to **I2C1_SDA** (Pin PB9)
   - **INT1** and **INT2** (Optional, for interrupt-driven operation) Not used for this scope

2. **UART Connection**:
   - **Tx** (Pin PA2) to your UART receiving device.
   - **Rx** (Pin PA3) to your UART receiving device.

### Software Setup

1. **Clone this repository**:
   ```bash
   git clone https://github.com/WassimHedfi/adxl345-driver-stm32.git
2. **Open the project in STM32CubeIDE.**
3. **Build and flash the project to your STM32 Nucleo-F446RE.**

## Code Structure

- **`ADXL345.c`**: Implementation of the ADXL345 driver functions.
- **`ADXL345.h`**: Header file containing function prototypes and definitions.
- **`main.c`**: Main application code for reading acceleration data and sending it over UART.

## Usage

1. Initialize the I2C and UART peripherals in `main.c`.
2. Use the provided functions in `ADXL345.c` to configure the sensor and read acceleration data.
3. Transmit the acceleration data using UART for real-time monitoring.

