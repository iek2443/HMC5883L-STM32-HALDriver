

# HMC5883L-STM32-HAL-Driver

A lightweight, modular and well-documented driver for the **HMC5883L** 3-Axis Digital Compass Sensor using the **STM32 HAL** I2C interface.

---

## ✨ Features

- ✅ Reads magnetic field data (X, Y, Z axes)
- ✅ Gain, averaging, data rate, and bias configuration
- ✅ Single and continuous measurement support
- ✅ ID verification
- ✅ Compatible with all STM32 series via HAL
- ✅ Clean, modular C code with Doxygen-style documentation

---

## 🔧 Requirements

- STM32 HAL library (e.g., `stm32f4xx_hal.h`, `stm32g0xx_hal.h`, etc.)
- I2C communication enabled
- HMC5883L connected to an I2C bus (default 7-bit address: `0x1E`)

---

## ⚙️ Configuration

You **must define and assign** the I2C handle used by the HMC5883L sensor.

### In the `.h` file:
```c
#include "stm32f4xx_hal.h"       // Use your MCU-specific HAL include
extern I2C_HandleTypeDef hi2c1;
static I2C_HandleTypeDef *hmc_port = &hi2c1;
```
## 🚀 Usage Example
```c
#include "HMC5883L.h"

hmc_t compass;

int main(void) {
    HAL_Init();
    MX_I2C1_Init(); // Initialize your I2C peripheral

    HMC5883L_Init();

    while (1) {

        HMC_Make_Measurement_4_Single();       // Trigger single measurement
        HAL_Delay(6);                          // Wait for data to be ready
        HMC_Read_All(&compass);                // Read and store all data
        HAL_Delay(1000);
    }
}
```
