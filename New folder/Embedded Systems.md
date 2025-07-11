The technical and technological information from the provided sources is as follows:

### 1. Hardware Platform Design and Components

A **hardware platform** comprises physical components defining a device's functionality. These platforms can be **integrated** (e.g., a **system-on-chip** with all components on a single integrated circuit) or **modular** (e.g., a **system on a module** where components are connected to one main module with potential for additional extension platforms).

Factors influencing hardware platform design include:
*   **Application type, constraints, and budget**: These dictate the choice of **microcontrollers** or **CPUs**.
*   **Specialized applications**: May incorporate **Graphical Processing Units (GPUs)** and **Digital Signal Processors (DSPs)**.
*   **Power source**: Whether **line-powered** or **battery-powered** affects the selection of computing modules.
*   **Connectivity**: Choices between **wired** and **wireless solutions** are based on desired **throughput** and **energy constraints**.
*   **Peripheral interaction**: Influences the choice of **I/O interfaces**, such as **General-Purpose I/O (GPIO)** or **serial interfaces** like **I2C** or **SPI**.
*   **Debugging method**: Must be factored into the design for **software development and testing**.

### 2. Memory Technologies

Memory is categorized into two main types:
*   **Volatile memory**: Contents are lost when power is removed. Examples include **Dynamic Random Access Memory (DRAM)** and **Static Random Access Memory (SRAM)**.
*   **Non-volatile memory**: Contents persist when power is removed. Examples include **Electronically Erasable, Programmable, Read-Only Memory (EEPROM)** and **Flash memory**.

**Characteristics and Use Cases**:
*   **Non-volatile memory** stores **persistent data**, such as **program code** for the microcontroller, **configuration data**, and **long-term or sensitive program data** generated during runtime.
*   **Volatile memory** stores **transient data**, such as **short-term program data** or program variables.
*   **EEPROM** is **byte-erasable**, allowing individual bytes to be addressed, erased, and rewritten. It is typically used for **program data** that may change at runtime, enabling fine-grained access.
*   **Flash memory** is **block-erasable**, meaning modifications occur in blocks of bytes. It is typically used for **program code** that does not change at runtime.
*   **DRAM** is generally **cheaper** but **slower** than **SRAM**, and requires periodic refreshing.
*   **SRAM** is **expensive** but **faster** and does not require refreshing. The trade-off is between cost and speed.

A typical microcontroller memory architecture, such as the **STM32L053C6 (Arm Cortex-M0+ architecture)**, might include a combination: 64 kilobytes of **Flash**, 2 kilobytes of **EEPROM**, and 8 kilobytes of **SRAM**. To accommodate large program code within small Flash memory, **architectural optimizations** like **compressed instruction sets** and **software-based optimizations** at code compilation time are adopted.

### 3. Sensors and Input/Output (I/O)

**Sensors** are **input devices** that convert a physical property of the environment into an **electrical signal**. This conversion often exhibits a **linear relationship** between the physical property and the electrical signal. For example, a light sensor converts photons into a voltage. The **sensitivity** of a sensor indicates the minimum input value required to produce a certain output signal.

**Types of Sensors**:
*   **Push buttons** (for user input)
*   **Temperature sensors** (for environmental measurement)
*   **Acceleration sensors** (for detecting direction and movement)
*   **Pressure sensors**
*   **Optical sensors**
*   **Humidity sensors**
*   **Force sensors**
*   **Microphones**

**Input/Output (I/O)** defines how a microcontroller interacts with its environment. Different I/O protocols are available:
*   **Universal Asynchronous Receiver Transmitter (UART)**: A simple two-wire serial communication protocol for data transfer between two devices.
*   **Serial Peripheral Interface (SPI)**: A serial bus enabling communication among multiple devices.
*   **Inter-Integrated Circuits (I2C)**: Similar to SPI, but uses a different physical layer and combines features of UART and SPI.
*   **General Purpose I/O (GPIO)**: The most straightforward I/O type, representing a simple on/off signal. GPIO pins can be configured to accept or source different logic voltage levels, allowing the microcontroller to control peripherals or receive external inputs/interrupts. Pins configured for interrupts can **wake up a microcontroller from low-power or sleep modes**. GPIO pins can be grouped into **GPIO ports** for collective control.
*   **Pulse-Width Modulation (PWM)**: Allows a GPIO port to be activated at a certain frequency, employed for controlling linear processes like fans or motors.
*   For driving higher current applications beyond GPIO's low current limit, **transistors** and **relays** are used.

### 4. Signal Conversion

*   **Analog signal**: A **continuous signal** that varies over time, capable of taking an infinite number of values between its minimum and maximum. Sensors often generate analog signals as varying voltages.
*   **Digital signal**: A **discrete signal** that takes on one of two values (ON/HIGH/1 or OFF/LOW/0).

**Analog-to-Digital Conversion (ADC)**:
*   Microcontrollers do not directly operate on analog signals. An **Analog-to-Digital Converter (ADC)** is used to convert analog signals into digital signals. ADCs are often built into microcontrollers.
*   The two main components of ADC are **sampling** and **quantization**.
    *   **Sampling**: Reading the analog signal's value at regular instances, determined by the **sampling frequency**.
    *   **Quantization**: Breaking the continuous range of analog values into discrete values.
*   The **resolution** of an ADC, measured in **bits**, indicates the number of discrete values it can generate. A higher number of bits represents more values and thus greater resolution.

**Digital-to-Analog Conversion (DAC)**:
*   The reverse process of ADC, converting a digital signal into an analog signal. The output analog signal can be a simple voltage level (e.g., for fan/motor control) or a complex waveform (e.g., radiofrequency).
*   Performance indicators for DACs include:
    *   **Dynamic range**: The difference between the largest and smallest signals produced.
    *   **Resolution**: The number of output levels that can be reproduced.
    *   **Total Harmonic Distortion and Noise (THD+N)**: Indicated in the DAC's datasheet.

### 5. Power Management

Several factors influence a hardware platform's **energy consumption**: power drained by the microcontroller (MCU), active time of the MCU, heat dissipation, and environmental temperature. A processor with higher power drain but less frequent activity can be more energy efficient.

**Power Saving Techniques**:
*   **Peripherals can be switched off** when not required.
*   **Microcontrollers can enter sleep modes** to temporarily disable functionality, reducing active time and power consumption. Deeper sleep modes offer greater power reduction but incur longer wake-up times and fewer wake-up sources (external interrupts).
*   **Wireless interfaces can be switched off** when not actively communicating; for example, **Bluetooth Low Energy** implements this, and **Wi-Fi** has a power-saving mode where the RF transceiver wakes periodically.
*   **Dynamic Voltage Frequency Scaling (DVFS)**: Modern microcontrollers can reduce or enhance performance based on task complexity. For computationally intensive tasks, voltage and frequency are increased, leading to higher power draw; subsequently, they are reduced to lower power draw.
*   **Software optimizations**: Compiling code with optimizations can minimize energy usage.
*   **Chip design**: Smaller chips with fewer transistors consume less energy.

### 6. Lab-Specific Technical Details (ST Disco L475VG & Mbed Ecosystem)

The lab utilizes the **ST Disco L475VG development board**. Its specifications include [L475VG-board-specifications]:
*   **Storage**: 64-Megabit quad-SPI flash memory.
*   **Connectivity**: Bluetooth V4.1 module, sub-Gigahertz low-power-programmable RF module, Wi-Fi module, dynamic near-field communication tag.
*   **Input/Output (On-board Sensors)**: Two digital omnidirectional microphones, capacitive digital sensor for relative humidity and temperature, 3-axis magnetometer, 3D accelerometer, 3D gyroscope, digital output barometer, time-of-flight and gesture detection sensor, two push-buttons.
*   **Communication**: USB on-the-go with Micro-A/B connector.
*   **Expansion**: Arduino Uno V3 and P MOD connectors.
*   **Power Supply**: Flexible options including ST LINK USB VBUS or external sources.
*   **Debugging**: On-board ST-LINK debugger/programmer with USB re-enumeration (mass storage, virtual com port, debug port).
*   **Pinout**: Physical connections where pins can be configured in software for different functions, including grouped functions like SPI or I2C.

The **Arm Mbed development ecosystem** is used for software development [Mbed-ecosystem]. The **Keil Studio Cloud** (browser-based) serves as the **Integrated Development Environment (IDE)** for IoT, machine learning, and embedded systems application development [Keil-Studio].

**Board Programming Process**:
*   Connecting the board via USB makes it appear as a **removable disk drive** (e.g., "DAP LINK") [board-programming].
*   **Programming** involves copying the **compiled program** (a ".bin" file) to this virtual disk drive [board-programming].
*   **Firmware update procedure**: Disconnect the board, hold reset, reconnect USB (drive appears as "CRP DISABLED"), delete the existing firmware file, copy the new "firmware.bin" file, then power cycle [firmware-update].
*   Within Keil Studio Cloud, programs are created or imported (e.g., "mbed os example blinky"). After selecting the target board, the "build program" button compiles code into a ".bin" file, and the "run program" button builds, copies, and executes the program on the board [Keil-Studio-workflow].

### 7. Lab Exercise Program Structure and Concepts

The lab exercise involves interfacing with on-board environmental sensors using the board and **Mbed API**. Data from sensors will be read and transmitted to a PC via **UART** for display on a terminal emulator.

**Key Program Components and Concepts**:
*   **APIs Used**: **'Buffered Serial' API** for PC communication, and an array of functions for interacting with **on-board sensor functions** (initialization, data reading).
*   **Project Setup Requirements**: Inclusion of **board support files** (to access sensor APIs) and enabling **floating-point support in 'printf' output** by setting 'minimal printf enable 64 bit' in the 'mbed lib dot jason' file.
*   **Program Objective**: Read temperature, humidity, pressure, magnetometer, accelerometer, and gyroscope values every three seconds; convert temperature to Fahrenheit and Kelvin; blink an LED every second; and enter sleep mode while waiting for interrupts. Sensor readings are inspected via the **serial debug interface**.
*   **Global Variables**:
    *   A **'buffered serial' object** for PC communication.
    *   A **'digital out' object** for the LED.
    *   Two **'low power ticker' objects** for tracking events: one for LED flashing (every second) and one for triggering sensor readings (every three seconds).
    *   A flag variable (e.g., `should read sensors`) to signal when measurements need to be read and displayed.
*   **Initialization**: Sensors are initialized, a welcome message is printed, and tickers are activated. The `initialise sensors` function calls required initialization functions for each sensor.
*   **Ticker Handlers**:
    *   `led tick` function: Toggles the LED state.
    *   `read out tick` function: Sets the `should read sensors` flag.
    *   Tickers are initialized and functions are attached to them.
*   **Main Function Loop**:
    *   Checks if the `should read sensors` flag is true.
    *   If true, calls a function to read from sensors, converts temperature data, writes output to **UART**, and clears the flag.
    *   Enters **sleep mode**.
    *   The LED should toggle its state every second, demonstrating responsiveness.

This structure ensures periodic sensor data acquisition, processing, communication, and power management through sleep modes.
