# STM32-Based Automatic Wiper System using Servo Motor

This project demonstrates how to control a **servo motor using STM32 (TIM1 PWM on PA9)**, simulating an automatic windshield wiper system. The servo sweeps from 0° to 180° and back in a loop, useful for rain-sensing or auto wiper applications.

---

##  Features

- Uses STM32 microcontroller with HAL libraries
- PWM signal generation using TIM1 Channel 2 (PA9)
- Servo sweeps smoothly from 0° to 180° and back
- Adjustable delay and sweep control
- Can be extended with rain sensor input

---

##  Project Overview

This example generates a PWM signal on **PA9 (TIM1_CH2)** to control a servo motor. The motor simulates a wiper blade sweeping left and right continuously with smooth motion using delays between angle changes.

---

## Components Required

| Component             | Quantity |
|-----------------------|----------|
| STM32F070RB / Blue Pill / STM32 Nucleo | 1        |
| SG90 Servo Motor      | 1        |
| Jumper Wires          | As needed |
| USB Cable (for ST-Link) | 1        |
| STM32CubeIDE          | Installed on PC |

---

## Pin Configuration

| STM32 Pin | Function        |
|-----------|------------------|
| PA9       | TIM1_CH2 (PWM)   |
| GND       | Servo GND        |
| 5V        | Servo VCC        |

---

##  How It Works

- TIM1 is configured with:
  - Prescaler: `960`
  - Period: `1000`
- PWM output is on `PA9` using TIM1 Channel 2
- `__HAL_TIM_SET_COMPARE()` adjusts duty cycle to move servo from ~0° (pulse=25) to ~180° (pulse=125)
- Servo is held briefly at each end for realism

---

## Code Snippet

```c
for (uint16_t pulse = 25; pulse <= 125; pulse++) {
    __HAL_TIM_SET_COMPARE(&htim1, TIM_CHANNEL_2, pulse);
    HAL_Delay(15);
}
