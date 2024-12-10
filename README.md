# Automated Jar Labeling System

This project automates the labeling process for marmalade jars using a custom-designed gripping and rotating mechanism. Integrated with an INTREX 200+ labeling machine, this system allows efficient, high-precision application of stickers around jars using sensors, stepper motors, and a Raspberry Pi with an Arduino controller. 

## Project Overview

The labeling system performs the following steps:
1. **Jar Detection**: An optical sensor detects when a jar is in place on the conveyor.
2. **Gripping**: A motorized gripper descends, captures the jar, and raises it to labeling height.
3. **Labeling & Rotation**: The INTREX 200+ is triggered to apply the sticker while the jar rotates to achieve full coverage.
4. **Return & Release**: The gripper lowers the jar and releases it, allowing the process to repeat.

## System Components

The primary components of the project include:

- **Control Board**: Arduino Mega 2560 for motor and sensor control.
- **Step Motors**: NEMA 17 motors for gripping and rotating.
- **Linear Actuator**: For height adjustments, synchronized with the INTREX labeling process.
- **Sensors**: Optical sensor to detect jar presence.
- **Labeling Machine**: INTREX 200+ (preset to constant output speed).
- **Camera (Optional)**: High-resolution USB camera for calibration.

### Bill of Materials

| Component               | Quantity | Description                       |
|-------------------------|----------|-----------------------------------|
| Arduino Mega 2560       | 1        | Microcontroller for system control |
| NEMA 17 Stepper Motors  | 2        | For jar rotation and gripping    |
| A4988 Stepper Drivers   | 2        | Motor drivers for NEMA 17s       |
| Optical Sensor          | 1        | Detects jar presence             |
| Linear Actuator (12V)   | 1        | Adjusts jar height               |
| Relay Module (4-Channel)| 1        | For gripper control              |
| Wiring & Connectors     | -        | For power and signal connections |

## Installation

1. **Hardware Setup**:
   - Assemble the frame and mount the gripper and actuator.
   - Connect the INTREX trigger to the control pins on the Arduino.
   - Wire the sensor and stepper motors to the Arduino, ensuring secure connections for power and signal.

2. **Software Setup**:
   - Load the provided C++ and Arduino code onto the Raspberry Pi and Arduino, respectively.
   - Install required libraries on the Raspberry Pi (`RPi.GPIO` for GPIO control).

3. **Calibration**:
   - Position a jar in the gripper, adjust the camera (if used), and test initial runs to refine alignment with the INTREX output.
   - Adjust rotation and actuator speed parameters in the code for precise labeling.

## Operation

- Place a jar on the conveyor belt in the sensor’s detection range.
- The system will automatically lower the gripper, grip the jar, lift it, and trigger the INTREX labeling process.
- The jar will rotate to apply the label evenly and then be released back onto the conveyor.

## Code Explanation

### C++ Code

The C++ code, running on a Raspberry Pi, handles the main sequence:
- **Jar Detection**: When a jar is detected, the process initiates.
- **Actuator Control**: The linear actuator lowers the gripper and adjusts height.
- **Rotation Control**: The jar is rotated by the stepper motor in sync with the INTREX speed.
- **INTREX Trigger**: A single pulse initiates the labeling process.

### Arduino Code

The Arduino code interprets commands from the Raspberry Pi and manages motor control, ensuring precise height and rotation adjustments. 

## Future Enhancements

1. **Automated Calibration**: Use the camera feedback to adjust alignment automatically.
2. **User Interface**: Add buttons to start, stop, and manually calibrate the process.
3. **Data Logging**: Record operational data for maintenance and analysis.

Explanation of Key Additions:

    Enable/Disable All Stepper Drivers: ENABLE_PIN is used to activate/deactivate all stepper drivers with enableDrivers() and disableDrivers().
    Process Flow Adjustments:
        A new step is added to lower, grip, lift, rotate, and release the jar.
        Calibration Factors (calibrationFactorHeight and calibrationFactorRotation) can be adjusted to fine-tune the speed and positioning.

This code will control the labeling process with each part of the sequence enabled by the stepper motors, and the power usage optimized by disabling drivers when not needed.

## License

This project is open-source and available for modification. Please acknowledge the project’s contributors if republished.

---

This README provides comprehensive guidance, from assembly through operation, for anyone setting up the automated jar labeling system.
