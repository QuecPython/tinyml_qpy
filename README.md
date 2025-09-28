# TinyML Gesture Recognition System

A real-time gesture recognition system using MPU6500 IMU sensor and Random Forest classifier on QuecPython embedded platform.

## System Overview

This TinyML system detects hand movements in real-time using machine learning directly on embedded hardware. The system uses a small sensor called MPU6500 that measures movement and rotation, currently optimized for X and Y axis movements.

## Features

- **Real-time Detection**: 150-300ms response time for gesture recognition
- **Memory Efficient**: Automatic buffer management with overflow prevention
- **False Positive Prevention**: Requires 3 consecutive results before detection
- **Timer-based Processing**: Non-blocking hardware timer architecture
- **Gesture Separation**: Each gesture analyzed independently without contamination

## Directory Structure

```plaintext
tinyml_qpy/
├── media
├── src
    ├── _main.py              # Main application with Timer-based system
    ├── mpu6500.py            # MPU6500 sensor driver with m/s² scaling
    ├── random_forest.py      # Pre-trained Random Forest model
    ├── tinyml.py             # TinyML pipeline with debounce mechanism
    ├── data_collect.py       # Data collection utility
├── LICENSE
├── README.md
└── README_zh.md
```

## Technical Details

- **Platform**: Quectel embedded module running MicroPython
- **Sensor**: MPU6500 6-axis IMU (3-axis accelerometer + 3-axis gyroscope)
- **Model**: Random Forest classifier (4 classes: 0=no gesture, 1-3=gesture types)
- **Sampling**: 50Hz sensor reading, 20Hz inference
- **Detection**: 3 consecutive results within 450ms window
- **Data Format**: Accelerometer (m/s²), Gyroscope (deg/s)

## Current Status

- **X/Y axis movements** - Working reliably with stable detection
- **Memory management** - Buffer contamination issues resolved
- **Real-time processing** - Timer-based architecture implemented
- **Debounce system** - False positive prevention working
- **Circular movements** - Currently under development

## Quick Start

### Prerequisites

Before getting started, ensure you have the following prerequisites:

- Hardware:
  - Prepare any Quecpython development board
  - Computer (Windows 7, Windows 10, or Windows 11)
  - MPU6500 sensor
- Software:
  - Debugging tool [QPYcom](https://developer.quectel.com/wp-content/uploads/2024/09/QPYcom_V3.9.0.zip)
  - QuecPython firmware (beta firmware is available in the `fw` directory of the repository)
  - Python text editor (e.g., [VSCode](https://code.visualstudio.com/), [PyCharm](https://www.jetbrains.com/pycharm/download/))

### Installation

1. **Clone the Repository:**

   ```
   git clone https://github.com/QuecPython/tinyml_qpy.git
   ```

2. **Flash the Firmware:** Follow the [instructions](https://developer.quectel.com/doc/quecpython/Getting_started/en/4G/flash_firmware.html) to flash the firmware onto the development board.

### Running_Application

1. **Hardware Connection:**  Correctly connect the MPU6500 sensor to the I2C interface of the development board.
2. **Connect to the host computer via Type-C.**
3. **Download the Code to the Device:**
   - Launch the QPYcom debugging tool.
   - Connect the data cable to the computer.
   - Press the **PWRKEY** button on the development board to power on the device.
   - Follow the [instructions](https://developer.quectel.com/doc/quecpython/Getting_started/en/4G/first_python.html) to import all files from the `src` folder into the module's file system, preserving the directory structure.
4. **Run the Application:**
   - Select the `File` tab.
   - Choose the `_main.py` script.
   - Right-click and select `Run` or use the `Run` shortcut button to execute the script.
5. For a usage example, refer to the demo video: `media/TinyML.mp4`

## Usage

The system automatically detects gestures in real-time. When a gesture is recognized, it outputs the classification result (1, 2, or 3) and clears all buffers to prevent contamination from previous gestures.

## Performance

- **Detection Latency**: 150ms theoretical minimum, 200-300ms practical
- **Memory Usage**: <50KB total
- **Accuracy**: Optimized for X/Y axis movements
