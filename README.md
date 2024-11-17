# Ambient Lighting using STM32 and LDR

In this project, we create an STM32-based ambient light sensor using an LDR (light-dependent resistor) to sense the ambient light intensity and map it to an LED's brightness. As the surroundings get darker, the LED brightness automatically increases, demonstrating a real-time light control system.

## Project Overview

This project involves:
- Measuring ambient light intensity using an LDR.
- Mapping the sensed light levels to PWM duty cycle values.
- Adjusting LED brightness based on the ambient light levels.

## Table of Contents
- [Required Components](#required-components)
- [Project Setup](#project-setup)
- [STM32 ADC Polling with PWM Control](#stm32-adc-polling-with-pwm-control)
- [Code Explanation](#code-explanation)
- [Testing the Project](#testing-the-project)

## Required Components

For this project, you'll need:
- STM32F103C8T6 board
- ST-Link v2 Debugger
- Breadboard
- LDR (Light Dependent Resistor)
- LED
- Resistors
- Jumper wires
- 9V Battery or DC power supply

## Project Setup

### Step 1: Set Up the STM32 Project
1. **Open STM32CubeMX** and create a new project.
2. **Select the Target MCU** - STM32F103C8T6.
3. **Configure ADC1 Peripheral**:
   - Enable Channel 7 (connected to the LDR) in single conversion mode.
   - Set software triggering for Channel 7.
4. **Configure Timer2 in PWM Mode**:
   - Set Timer2 to operate in PWM mode with output on Channel 1 (connected to the LED).
5. **Set System Clock** to 72 MHz.

### Step 2: Hardware Connections
- **LDR Circuit**: Connect the LDR in series with a resistor to form a voltage divider, where the voltage across the resistor will vary based on the ambient light intensity.
- **ADC Pin**: Connect the voltage divider output to the ADC input pin (Channel 7).
- **LED Circuit**: Connect the LED with a current-limiting resistor to Timer2 PWM output (Channel 1).


## STM32 ADC Polling with PWM Control

This project uses ADC polling to read the LDR value, calculate a PWM duty cycle, and output it to an LED. Here’s how it works:

1. **Ambient Light Level Calibration**: On startup, the system reads the initial ambient light level as a baseline.
2. **Real-Time Brightness Adjustment**: As light intensity changes, the LDR’s resistance changes. The ADC reads these variations, and the PWM duty cycle adjusts to brighten the LED as the environment darkens.

### Code Explanation
1. **System Initialization**: The code sets up system clock, GPIO, ADC, and PWM peripherals.
2. **Ambient Light Calibration**: Reads the ambient light level and sets it as a base level for calculations.
3. **Real-Time Adjustment**: In the infinite loop, the ADC continuously reads the current light level, calculates the PWM duty cycle, and adjusts LED brightness based on ambient light intensity.

## Testing the Project

1. **Power-Up Calibration**: Ensure the LDR is in a well-lit environment when powering up.
2. **Real-Time Adjustment**: Observe the LED brightness as you vary the ambient light. The LED should brighten as the environment darkens.
