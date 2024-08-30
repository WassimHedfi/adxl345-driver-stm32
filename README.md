# ADXL345 Driver for STM32 Nucleo-F446RE

This repository provides a custom driver for the ADXL345 accelerometer, designed for seamless integration with the STM32 Nucleo-F446RE board. The driver is implemented as a modular set of source and header files, facilitating straightforward deployment and adaptation across various STM32 boards and microcontrollers.

##  🚀 Features

- **Efficient ADXL345 Driver 📡**:Lightweight and optimized driver for the ADXL345 accelerometer, enabling reliable I2C communication.
- **I2C Communication 🔄**: Manages setup and data exchange with the ADXL345 using the I2C protocol.
- **UART Data Transmission 📊**: Reads acceleration data (`x_acc`, `y_acc`, `z_acc`) from the ADXL345 and transmits it via UART for real-time monitoring or further processing. 
- **Modular Architecture 🧩**: Organized into separate source and header files for ease of integration into different projects or STM32 microcontrollers.

## 🛠️ Getting Started

### Prerequisites

- **[STM32 Nucleo-F446RE](https://www.st.com/en/evaluation-tools/nucleo-f446re.html)**: The target microcontroller board for this project.
- **[ADXL345 Accelerometer](https://www.analog.com/media/en/technical-documentation/data-sheets/ADXL345.pdf)**: A 3-axis accelerometer with I2C communication.
- **[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)**: Recommended IDE for development and compilation.
- **UART Interface**: For monitoring or processing the accelerometer data on a connected device.

### ⚙️ Hardware Setup

1. **Connect the ADXL345 to the STM32 Nucleo-F446RE**:
   - **VCC** to **3.3V**
   - **GND** to **GND**
   - **SCL** to **I2C1_SCL** (Pin PB8)
   - **SDA** to **I2C1_SDA** (Pin PB9)
   - **INT1** and **INT2** (Optional, for interrupt-driven operation) not utilized in this scope.

2. **UART Connection**:
   - **Tx** (Pin PA2) to your UART receiving device.
   - **Rx** (Pin PA3) to your UART receiving device.

### 📥 Software Setup

1. **Download the [core folder](Core)** containing necessary files
2. **Open STM32CubeIDE** and setup your MXConfigurations with I2C1 at pins PB8 & PB9 and make use of USART2 on the Asynchronous mode
3. **Include driver files** in your project:
* [`ADXL345.c`](Core/Src/ADXL345.c) in the [`Src`](Core/Src) directory
* [`ADXL345.h`](Core/Inc/ADXL345.h) in the [`Inc`](Core/Inc) directory
4. **Replace or adjust** your [`main.c`](Core/Src/main.c) file as needed
5. **Build and flash** the project to the STM32 Nucleo-F446RE.

## 📂 Code Structure

- **[`ADXL345.c`](Core/Src/ADXL345.c)**: Contains implementation details for the ADXL345 driver functions.
- **[`ADXL345.h`](Core/Inc/ADXL345.h)**: Defines function prototypes and constants.
- **[`main.c`](Core/Src/main.c)**: Hosts the application code responsible for reading acceleration data and transmitting it via UART.

## ⚙️ Usage

1. **Initialize** the I2C and UART peripherals in `main.c`.
2. **Configure** the ADXL345 sensor and retrieve acceleration data using functions from `ADXL345.c`.
3. **Transmit** acceleration data over UART for real-time monitoring.

### Example Code

```c
#include "ADXL345.h"

// Initialize peripherals
MX_I2C1_Init();
MX_USART2_UART_Init();

// Initialize ADXL345
ADXL345_Init();

// Main loop
while (1) {
    float x_acc, y_acc, z_acc;
    
    // Read acceleration data
    TT_GET_ACCELERATIONS();
    
    // Send data over UART
    printf("X: %f, Y: %f, Z: %f\n", x_acc, y_acc, z_acc);
    
    HAL_Delay(500); // Adjust delay as needed
}
```

---

📌 **N.B.**
Note that the `ADXL345.c` driver file includes two functions for obtaining acceleration data: one for basic data retrieval and another, used in `main.c`, that converts the data into a string buffer, preparing it for transmission over UART.
